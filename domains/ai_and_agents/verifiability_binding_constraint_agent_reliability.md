---
name: Verifiability Is the Binding Constraint for Agent Reliability, Not Model Intelligence
domain: ai_and_agents
tier: core
confidence: medium-high
source: Claire Vo (OpenClaw) + Simon Willison via Lenny's Newsletter (Mar 29 - Apr 2, 2026)
created: 2026-04-05
reverify_by: 2026-07-05
tags: [agent-reliability, verification, workflow-selection, testing]
---

## Pattern

Agents perform consistently in domains where output can be verified fast and unambiguously. The bottleneck for agent work has shifted from generation to testing. Code is uniquely suited because it's demonstrably right or wrong.

## Evidence

Simon Willison (Lenny's Apr 2): three agentic engineering patterns all center on verification:
- Red/Green TDD = verifiable output contract
- Templates = verifiable scaffold
- Hoarding = cataloguing what's known to work

"Vibe coding is fine if the only person harmed by bugs is you. The moment you ship it for others, take a step back."

## Decision Rule

Prioritize automating domains with fast, unambiguous feedback loops:
- **High verifiability (automate first):** Data pipelines, testing, reporting, structured data extraction, code generation
- **Low verifiability (automate last):** Legal strategy, creative direction, relationship management, contested-correctness domains

## Boundaries

- Automated test suites can be gamed — passing checks ≠ correct behavior in production
- Verifiability quality determines reliability ceiling
- Some domains can be made verifiable by adding structured evaluation criteria (e.g., rubrics for content quality)

## Transfer

Applies beyond AI: any quality assurance system, manufacturing inspection, financial auditing. The principle is universal — reliability scales with verification speed, not production capability.
