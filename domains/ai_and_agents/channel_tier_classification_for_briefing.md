---
name: Channel Tier Classification for Reading Priority
description: Classify communication channels into priority tiers using name patterns, then use tiers to control LLM analysis depth and brief framing
type: pattern
domain: ai_and_agents
source: First-party implementation — Slack EA project (production)
confidence: medium-high
date_added: 2026-03-24
tags: [briefing, signal-detection, classification, priority, llm-patterns, slack, automation]
related: [precomputed_metadata_for_llm_analysis.md, leadership_domain_sectioned_briefs.md]
---

## The Problem

Not all communication channels deserve equal attention in an automated brief. Leadership channels need immediate, careful analysis. Random social channels need a quick scan at most. Without tiering, the LLM either:
- Wastes tokens analysing low-priority channels in depth
- Treats everything with equal urgency, diluting real signals
- Produces briefs that are too long because every channel gets a mention

## The Pattern: Config-Driven Tier Classification

### Tier Definitions

Define tiers based on channel name patterns in configuration (not in code):

| Tier | Pattern Examples | Reading Priority | Brief Behaviour |
|------|-----------------|-----------------|-----------------|
| A — Leadership | `leadership-*`, `exec-*`, `strategy-*` | Highest — scan for anything Josh/CEO missed | Only flag missed items (Josh is likely already active here) |
| B — Team/Ops | `team-*`, `ops-*`, `internal-*` | High — operational health | Flag blockers, resource issues, decisions needed |
| C — Client | `client-*` | High — client relationship health | Flag unanswered messages, escalations, sentiment shifts |
| D — External | `external-*`, `partner-*` | Medium — external relationship management | Flag unanswered items, opportunities |
| E — Pod/Project | `pod-*`, `project-*` | Medium — execution tracking | Flag delays, blockers, milestones |
| F — Specialty | `design-*`, `dev-*`, `finance-*` | Lower — functional detail | Only flag cross-functional items or escalations |
| G — Other | Everything else | Lowest — background noise | Scan only, rarely surface items |

### How Tier Affects the System

1. **Message limits:** Higher tiers get more messages sent to the LLM (e.g., Tier A: all messages, Tier G: last 20)
2. **Items per tier in brief:** Higher tiers get more slots (e.g., Tier A-C: 5 items each, Tier F-G: 2 items max)
3. **LLM instructions vary by tier:** The system prompt includes tier-specific framing ("For Tier A channels, Josh is active — only flag items he may have missed")
4. **Signal interpretation:** An unanswered message in Tier C (client) is more urgent than the same signal in Tier G (other)

### Why Config-Driven

The classification logic is pure pattern matching — no ML needed. Keeping it in config means:
- Non-technical users can adjust tiers by editing a JSON file
- New channels are automatically classified when created (if they follow naming conventions)
- Tier definitions can vary per brief type (leadership briefs may use different tiers than MD briefs)

## Generalisation

This pattern applies to any system that processes multiple information streams with different priority levels:
- **Email triage:** Classify by sender domain, subject patterns
- **Ticket systems:** Classify by queue, priority tag, customer tier
- **Monitoring:** Classify alerts by service criticality

The principle: **classify inputs before the LLM sees them, then use the classification to control analysis depth and output allocation.**

## Where Applied

- **Slack EA project:** Channel tier classification in config, referenced by formatter and briefing logic

## Pitfalls

1. **Naming convention drift:** If teams create channels that don't follow patterns (e.g., `acme-project` instead of `client-acme`), they'll fall into Tier G. Periodically audit unclassified channels.
2. **Tier inflation:** Resist the urge to make everything Tier A-C. If most channels are "high priority," nothing is. Keep the distribution roughly: A (5%), B-C (20%), D-E (30%), F-G (45%).
3. **Context about the reader matters:** Tier A channels where the reader is already active need LESS analysis, not more. The brief should add value beyond what the reader already saw.
