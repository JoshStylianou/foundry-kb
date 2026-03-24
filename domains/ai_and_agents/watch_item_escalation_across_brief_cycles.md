---
name: Watch Item Escalation Across Brief Cycles
description: Stateful pattern for tracking watch items between LLM brief runs, with automatic escalation of persistent issues
type: pattern
domain: ai_and_agents
source: First-party implementation — Slack EA project (production)
confidence: high
date_added: 2026-03-24
tags: [briefing, llm-patterns, state-management, escalation, signal-detection, automation]
related: [structured_llm_output_via_tool_use.md, precomputed_metadata_for_llm_analysis.md]
---

## The Problem

In recurring brief/alert systems, "watch" items (things worth monitoring but not yet urgent) tend to sit in the watch category forever. Without memory across runs, each brief treats every watch item as if it appeared for the first time. Important signals that persist across multiple cycles never get escalated — they just keep appearing as "watch" until someone manually notices.

## The Pattern: Stateful Watch with Automatic Escalation

### Architecture

1. **State file** persists between brief runs (JSON file on disk or in a database):
   ```json
   {
     "watch_items": [
       {
         "channel": "client-acme",
         "summary": "No response to deliverables shared Tuesday",
         "first_seen": "2026-03-24T07:00:00Z",
         "occurrences": 2,
         "last_seen": "2026-03-24T12:00:00Z"
       }
     ]
   }
   ```

2. **At each brief run**, pass prior watch items to the LLM with explicit instructions:
   ```
   The following items were flagged as WATCH in previous briefs. For each:
   - If still unresolved based on current messages: ESCALATE to ACTION REQUIRED with escalated_from_watch=true
   - If resolved (reply received, issue addressed): DROP entirely — do not include
   - Do not re-add as a new watch item
   ```

3. **The LLM returns** structured output with an `escalated_from_watch` boolean flag on escalated items

4. **After each run**, update the state file: increment `occurrences` for persisting items, remove resolved ones, add new watch items from this cycle

### State File Design

Maintain **separate state files per brief type** (e.g., `state.json` for MD briefs, `leadership-state.json` for leadership briefs). Different brief types have different cadences and audiences — shared state causes cross-contamination.

### Escalation Rules

Keep escalation rules simple and explicit:

| Condition | Action |
|-----------|--------|
| Watch item appears in 2+ consecutive cycles | Escalate to ACTION REQUIRED |
| Watch item resolved (evidence in current messages) | Drop entirely |
| New issue detected this cycle | Add as WATCH |
| Previously escalated item still unresolved | Keep as ACTION REQUIRED |

## The Key Insight

The state file creates **temporal awareness** in a system that otherwise has no memory. Each brief run is stateless from the LLM's perspective — it processes the current window of messages. But by injecting prior watch items as context, you give the LLM the ability to detect persistence and escalate accordingly.

This is a general pattern: **inject prior state as LLM context to create temporal reasoning without fine-tuning or memory systems.**

## Where Applied

- **Slack EA project:** `config/state.json` (MD briefs) and `config/leadership-state.json` (Leadership briefs) — read at start of each brief run, updated after LLM response

## Pitfalls

1. **State file corruption:** If a brief run fails mid-write, the state file can be left in an inconsistent state. Write to a temp file, then atomic rename.
2. **Stale watch items:** Items can persist in the state file after the relevant channel goes quiet. Add a TTL — drop watch items older than X days (e.g., 7 days) regardless of resolution status.
3. **LLM ignoring prior watch:** If the prior watch items are buried in a long prompt, the LLM may not process them carefully. Place them prominently — immediately after the system prompt, before current message data.
4. **Escalation fatigue:** If too many items escalate simultaneously, the ACTION REQUIRED section loses urgency. Consider a cap (e.g., max 5 escalated items) with the rest remaining as high-priority watch.
