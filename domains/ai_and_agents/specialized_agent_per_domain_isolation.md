---
name: Specialized Agent Per Domain, Isolated Per Machine, Zero Credential Crossover
domain: ai_and_agents
tier: reference
confidence: medium
source: Claire Vo via Lenny's Newsletter (Mar 29 + Mar 31, 2026)
created: 2026-04-05
reverify_by: 2026-07-05
tags: [agent-architecture, security, isolation, personal-ai-os, multi-agent]
related: [lethal_trifecta_agent_security.md]
---

## Pattern

Running multiple specialized agents (one per function) on isolated hardware with separate accounts, read-only permissions by default, and no shared credentials produces a multi-agent system that is both more reliable and more auditable than a single general-purpose agent given broad access.

## Evidence

Claire Vo (Lenny's Mar 29 + Mar 31): 100+ hours hands-on across 9 dedicated agents on $600 Mac Mini M4 ($6–$50/month running cost). Each agent has:
- Own workspace, credentials, session storage
- Dedicated personality, model selection, tool permissions
- Zero data crossover between agents
- SOUL file for persistent memory
- Started read-only, graduated to write access per agent as trust was established

## Decision Rule

When architecting a personal or business AI OS:
- One agent per functional domain (not one agent with many tools)
- Isolated credentials per agent — no shared secrets
- Read-only by default, write access earned through trust
- Persistent memory via dedicated files, not shared context

## Boundaries

- Coordination overhead becomes significant when tasks require cross-agent context sharing
- The zero-crossover principle trades integration richness for isolation guarantees
- Single practitioner evidence — architecture is sound but not validated at enterprise scale
- The Foundry's own architecture already follows this pattern (separate Chiefs, isolated subagents)
