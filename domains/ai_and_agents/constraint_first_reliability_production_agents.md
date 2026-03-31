---
name: Constraint-First Reliability in Production Agents
description: Reliability at scale comes from deterministic structural brackets around LLM decisions, not from improving model judgment. Design failure modes first, build infrastructure to bound each one.
type: insight
domain: ai_and_agents
source: Stripe engineering blog, InfoQ coverage
confidence: high
date_added: 2026-03-31
date_verified: 2026-03-31
tags: [agents, reliability, production, deterministic-gates, safety-envelope]
related: [agentic_workflows_patterns.md, classifier_gated_permission_tiers.md]
---

## Core Pattern

In production autonomous agent systems, reliability at scale is achieved by surrounding LLM decision-making with deterministic structural brackets, not by improving model judgment. The agent operates freely inside the brackets; the infrastructure guarantees the safety envelope.

Architecture: fixed deterministic nodes alternating with open-ended LLM loops.

## Evidence: Stripe Minions

1,300 zero-human-written PRs/week at a company processing $1T+ in annual payments. 30% WoW growth (1,000 to 1,300 in ~2 weeks).

Specific brackets:
1. **Sandboxed devboxes** spin up in <10s, isolated from production data
2. **Curated tool subsets** — ~15 tools per task, deterministically prefetched from 400+ available, before agent activates
3. **Mandatory local lint gate** before code touches CI
4. **Hard 2-round CI retry cap** before human handoff
5. **Directory-scoped rule files**, not global context dumps

## When to Apply

Building any production agent that takes consequential or irreversible actions. Define what can fail before building; add a deterministic gate for each failure mode.

## Boundaries

- Requires pre-existing standardized infrastructure to sandbox within (inconsistent environments break the safety envelope)
- Substantial upfront infrastructure investment (Stripe's devbox reflects ~10 years of platform work)
- Doesn't apply to exploratory agents where deterministic gates are impossible
- Local gating only works when tests are fast and comprehensive

## Sources

- stripe.dev/blog/minions-stripes-one-shot-end-to-end-coding-agents-part-2
- infoq.com/news/2026/03/stripe-autonomous-coding-agents
