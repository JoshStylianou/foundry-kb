---
name: Leadership Domain-Sectioned Briefs
description: Pattern for generating multi-stakeholder LLM briefs where each leader sees only their domain, with CEO getting the cross-functional view
type: pattern
domain: ai_and_agents
source: First-party implementation — Slack EA project (production)
confidence: high
date_added: 2026-03-24
tags: [briefing, llm-patterns, leadership, multi-stakeholder, structured-output, slack]
related: [structured_llm_output_via_tool_use.md, precomputed_metadata_for_llm_analysis.md]
---

## The Problem

In organisations with multiple leaders, a single flat brief creates two failure modes:
1. **Information overload:** Each leader wades through items irrelevant to them
2. **Ownership ambiguity:** No one knows which items are "theirs" to act on

## The Pattern: Domain-Based Channel Routing

### Architecture

1. **Define leadership domains in config** — each leader is mapped to the channels they own:
   ```json
   {
     "domains": {
       "Creative Director": {
         "lead": "Jane Smith",
         "channels": ["design-*", "brand-*", "creative-*"]
       },
       "Head of Performance": {
         "lead": "John Doe",
         "channels": ["paid-*", "analytics-*", "client-*-perf"]
       }
     }
   }
   ```

2. **Channel classification function** routes each channel to the correct domain using pattern matching against the config

3. **LLM produces per-domain sections** — the tool schema includes a `domains[]` array where each domain has:
   - Domain name and lead
   - Status indicator (red/amber/green)
   - Action items and watch items scoped to that domain's channels only

4. **Cross-functional channels** (channels matching no domain pattern) appear ONLY in the CEO/top-level summary section — they are not assigned to any individual leader

### The Cross-Functional Rule

This is the key design decision: channels that span multiple domains (e.g., `#leadership`, `#all-hands`, `#strategy`) must NOT be duplicated across domain sections. They go in a separate top-level section visible to the overall recipient (typically CEO or MD). This prevents:
- The same issue appearing in three leaders' sections
- Confusion about who owns cross-functional items
- Bloated briefs from duplication

### Status Indicators

Each domain section gets a traffic-light status:
- **Red:** Action required items exist — something needs attention now
- **Amber:** Watch items exist — nothing critical but things to monitor
- **Green:** All clear — no items requiring attention

The status is derived from the items, not assigned by the LLM independently. If a domain has items in `action_required[]`, it's red. If only `watch[]`, it's amber. If neither, it's green.

## When to Use This Pattern

- Multiple stakeholders consuming the same information stream
- Clear domain/ownership boundaries exist
- You want focused, actionable output per person rather than a single long document
- The same underlying data (messages, tickets, metrics) needs different views

## Where Applied

- **Slack EA project:** Leadership briefs for TNT Growth — channels routed to Creative, Performance, Strategy, and Operations domains with CEO summary for cross-functional channels

## Pitfalls

1. **Domain boundaries are political, not technical.** Get sign-off on who owns what before building. Changing domain mappings after launch causes confusion.
2. **New channels need classification.** If someone creates `#client-acme-design`, which domain gets it — Creative or the client owner? Build a fallback rule (e.g., first matching pattern wins, or unmatched channels go to CEO summary).
3. **Domain sections with zero items still need to appear** — "all clear" is information. Don't hide empty domains; show them as green.
