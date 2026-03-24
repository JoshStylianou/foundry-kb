---
name: Knowledge Cascade — Retrieval Hierarchy for Advisory Agents
description: Six-level retrieval hierarchy, knowledge freshness heuristics, demand-driven KB growth loop
type: framework
domain: ai_and_agents
source: synthesis (AI Consultant Agent project)
confidence: high
date_added: 2026-03-22
date_verified: 2026-03-22
tags: [knowledge-management, retrieval-hierarchy, context-budget, advisory-agents, kb-curator]
related: [consulting_agent_architecture.md, claude_code_context_management.md]
---

## The Knowledge Cascade

Advisory agents must retrieve knowledge in a strict hierarchy. Never skip levels.

| Priority | Source | Cost | When |
|----------|--------|------|------|
| 1 | System prompt (constitutional) | Zero — already loaded | Always available |
| 2 | KB INDEX.md scan | ~200 tokens | Every question — fast check of coverage |
| 3 | Specific KB entry read | ~500-1000 tokens | When INDEX shows relevant entry |
| 4 | Memory / project files | ~300-1000 tokens | For user context and past decisions |
| 5 | WebSearch | ~500-2000 tokens + latency | When KB has no coverage or entry is stale |
| 6 | WebFetch | ~1000-5000 tokens + latency | When a search result needs deep extraction |

## Knowledge Freshness Heuristics

Different knowledge types have different shelf lives. The agent must apply the right source based on freshness requirements.

| Knowledge Type | Shelf Life | Source Priority |
|---------------|-----------|----------------|
| Architectural patterns | 6-12 months | KB then textbooks then papers |
| Specific model capabilities | 1-3 months | Live research then KB |
| Tool/API pricing and limits | 1-2 weeks | Live research only |
| Best practices for a specific tool | 3-6 months | KB then official docs then live research |
| New releases and announcements | Hours to days | Live research only |
| Business strategy frameworks | 12+ months | KB then established sources |

## Decision Logic

- **Specific tool/model question:** KB first. If entry is older than 30 days or missing, research live.
- **General pattern/principle:** KB is likely sufficient. Research only if KB has no relevant entry.
- **Pricing, availability, release dates:** Always research live.
- **"What's the best tool for X":** KB for evaluation framework, live research for current landscape.

## The Demand-Driven Knowledge Loop

The cascade creates a feedback loop between the advisory agent and the kb-curator:

1. Consultant checks KB, finds no coverage for topic X
2. Consultant researches live and advises the user
3. Consultant writes flag to `research_requests/consultant_flags.md`
4. kb-curator picks up flag on next cycle, writes proper KB entry
5. Next time topic X arises, consultant finds it at level 3 instead of level 5

This means the KB grows based on actual demand, not speculative coverage.

## Evidence

- Three-layer cognitive architecture: ArXiv 2603.10808 (Nurture-First Development, March 2026)
- Context Is Milk principle: progressive disclosure prevents context waste
- Knowledge freshness: derived from AI tool landscape volatility analysis

## Why This Matters to The Foundry

Every advisory agent (AI Consultant, future specialized consultants) should follow this cascade. It prevents redundant web research, respects context budgets, and makes the KB progressively more valuable. The cascade is how the KB transitions from "9 entries, mostly empty domains" to a comprehensive knowledge base — driven by what Josh actually asks about.

## Action Triggers

When building any agent that needs domain knowledge: encode the six-level cascade. When an advisory session reveals a KB gap: write to the research requests file. When the kb-curator runs: check research requests before starting autonomous research.
