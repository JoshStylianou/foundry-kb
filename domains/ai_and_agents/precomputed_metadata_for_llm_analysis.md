---
name: Pre-computed Metadata Pattern for LLM Analysis
description: Compute derived data (timestamps, counts, durations) before sending to the LLM to prevent hallucinated calculations and reduce tokens
type: pattern
domain: ai_and_agents
source: First-party implementation — Slack EA project (production)
confidence: high
date_added: 2026-03-24
tags: [llm-patterns, data-preparation, hallucination-prevention, signal-detection, briefing]
related: [structured_llm_output_via_tool_use.md]
---

## The Problem

LLMs are unreliable at:
- Calculating time differences ("this message was sent 4.5 hours ago")
- Counting items in long lists ("there are 23 messages in this thread")
- Deriving statistics from raw data ("average response time is 2.3 hours")
- Comparing timestamps across timezones

If you send raw message data to an LLM and ask it to identify "channels with no reply in 4+ hours," it will hallucinate the time calculations. The summaries will sound confident but the numbers will be wrong.

## The Pattern: Compute Before You Prompt

Calculate all derived metrics **in code** before sending data to the LLM. Include the pre-computed values as structured metadata that the LLM is explicitly told to trust, not re-derive.

### Implementation

1. **Compute metadata per data unit** (per channel, per thread, per document — whatever your unit of analysis is)
2. **Format as a structured line** the LLM can parse:
   ```
   [META] #channel-name | messages: 15 | threads: 3 | unanswered_external: 2 | last_tnt_reply: 6.2h ago | last_external_msg: 1.5h ago
   ```
3. **Instruct the LLM explicitly** in the system prompt:
   ```
   Trust the [META] values. Do not attempt to recalculate timestamps, message counts, or response times from the raw messages. Use the pre-computed values as ground truth.
   ```
4. **Include the raw messages** below the META line for context/summarisation, but the LLM's job is to interpret and prioritise, not calculate.

### What to Pre-compute

| Metric | Why Pre-compute |
|--------|----------------|
| Time since last message/reply | LLMs cannot do timezone-aware datetime math reliably |
| Message/thread counts | Counting is error-prone in long contexts |
| Unanswered message counts | Requires logic about who is "internal" vs "external" — don't make the LLM figure this out |
| Status flags (acknowledged, escalated) | Binary flags from code logic are more reliable than LLM inference |
| Duration calculations | Hours between events, SLA breach detection, etc. |

### The Division of Labour

| Task | Who Does It |
|------|-------------|
| Data retrieval | Code (API calls, database queries) |
| Metric calculation | Code (deterministic, testable) |
| Filtering and aggregation | Code (which channels to include, message limits) |
| Pattern recognition and prioritisation | LLM (what matters, what's urgent, what to escalate) |
| Natural language summarisation | LLM (writing the brief, framing the insight) |
| Formatting and rendering | Code (Slack mrkdwn, HTML, etc.) |

## Generalisation

This pattern applies anywhere you're feeding data to an LLM for analysis:

- **Customer support triage:** Pre-compute ticket age, response count, sentiment score — don't ask the LLM to derive these from raw ticket text
- **Code review:** Pre-compute diff size, files changed, test coverage delta — let the LLM focus on code quality, not counting
- **Sales pipeline:** Pre-compute days in stage, deal value, activity frequency — let the LLM identify risk patterns

## Where Applied

- **Slack EA project:** `computeChannelMetadata()` in `formatter.js` computes all per-channel metrics before LLM analysis

## Pitfalls

1. **Stale metadata:** If you pre-compute but then include messages that arrived after computation, the META values will be wrong. Compute metadata from the same snapshot you send to the LLM.
2. **Over-computing:** Don't pre-compute things the LLM actually is good at (sentiment, urgency, topic classification). Pre-compute what it's bad at (math, counting, time).
3. **META instruction drift:** If the system prompt doesn't explicitly tell the LLM to trust META values, it may try to "verify" them by counting messages itself — and get a different (wrong) number, causing confusion.
