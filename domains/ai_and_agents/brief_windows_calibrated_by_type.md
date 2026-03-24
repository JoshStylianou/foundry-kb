---
name: Separate Brief Windows Calibrated by Type
description: Different brief types need different lookback windows, message limits, and LLM instructions — calibrate each independently
type: pattern
domain: ai_and_agents
source: First-party implementation — Slack EA project (production)
confidence: high
date_added: 2026-03-24
tags: [briefing, llm-patterns, scheduling, configuration, automation, slack]
related: [structured_llm_output_via_tool_use.md, channel_tier_classification_for_briefing.md, watch_item_escalation_across_brief_cycles.md]
---

## The Problem

A single lookback window (e.g., "last 12 hours") does not work for a brief system that runs at different cadences. A morning brief needs to cover overnight activity. A midday brief only needs the last few hours. A weekend brief needs to cover Friday evening through Monday morning. Using the same window for all brief types either:
- Misses messages (window too short for weekend)
- Floods with duplicates (window too long for midday)
- Wastes tokens sending irrelevant old messages to the LLM

## The Pattern: Per-Type Configuration

### Window Definitions

Each brief type has independently calibrated parameters:

| Brief Type | Lookback Hours | Message Limit | Max Items/Tier | Char Limit | Framing |
|-----------|---------------|---------------|----------------|------------|---------|
| Morning | 10h | 100 | 5 | 3500 | "Overnight digest — what needs attention today" |
| Midday | 8h | 100 | 5 | 3500 | "Morning progress — what's changed since the morning brief" |
| End of Day | 6h | 100 | 5 | 3500 | "Day wrap — what carries over to tomorrow" |
| Weekend | 63h | 200 | 8 | 6000 | "Weekend catch-up — full picture of what happened" |
| Week Review | 105h | 200 | 8 | 6000 | "Week in review — patterns, themes, and strategic items" |

### What Scales with Window Size

When the lookback window is large (weekend, week review), multiple parameters need to scale proportionally:

1. **Message limit per channel:** More hours = more messages to include. A 63-hour window with a 100-message limit will miss things in active channels. Scale to 200.
2. **Max items per tier in the brief:** A larger window surfaces more signals. Allow more items (8 vs 5) or the brief will be artificially truncated.
3. **Character limit for the brief:** More items need more space. Scale the output limit so the LLM doesn't compress everything into terse summaries.
4. **LLM system prompt framing:** A weekend brief should explicitly frame as "catch-up" — the reader hasn't been online. A midday brief assumes the reader saw the morning brief.

### Timezone Considerations

Brief windows must align with the **reader's timezone**, not the server's timezone:
- UK morning brief at 07:00 BST looks back 10 hours (covers from 21:00 previous night)
- US Eastern leadership brief at 09:00 ET looks back to cover the US overnight gap
- Weekend brief window starts Friday 17:00 in the reader's timezone

Calibrate windows based on when the reader was last likely to be online, not based on round numbers.

## Where Applied

- **Slack EA project:** MD briefs calibrated to UK timezone (Europe/London), Leadership briefs calibrated to US Eastern (America/New_York), with separate window configs for each type

## Pitfalls

1. **Overlapping windows:** If morning lookback is 10h and the previous EOD brief was 8h ago, there's a 2h overlap. This is fine — slight overlap is better than gaps. But the LLM may re-flag items from the previous brief. Use the watch-item state to deduplicate.
2. **DST transitions:** A "10 hour lookback" means different things when clocks change. Use timezone-aware datetime libraries and test around DST boundaries.
3. **Large windows and token cost:** A 63-hour weekend window with 200 messages per channel across 50 channels is a lot of tokens. Budget for it — these runs will cost 3-5x a normal brief run.
