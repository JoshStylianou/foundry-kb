---
name: Deterministic Orchestration Must Be Architecturally Separate From Autonomous Reasoning
domain: ai_and_agents
tier: reference
confidence: medium-high
source: CrewAI Flows architecture (blog.crewai.com/agentic-systems-with-crewai/)
created: 2026-04-05
reverify_by: 2026-07-05
tags: [orchestration, agent-architecture, deterministic, production-systems]
related: [agentic_workflows_patterns.md]
---

## Pattern

Production multi-agent systems that mix deterministic control flow with autonomous reasoning degrade both. Explicit separation produces independently improvable, auditable, recoverable systems.

- **Crews** = autonomous reasoning (agents decide how to accomplish a goal)
- **Flows** = deterministic orchestration (code defines sequence, routing, error handling)

## Evidence

CrewAI Flows architecture validated at 12M+ executions/day as of 2026.

## Decision Rule

For any multi-step agent pipeline going to production:
- Deterministic parts (sequence, routing, retries, error handling) belong in code, not in prompts
- Autonomous parts (reasoning, generation, analysis) belong in agent prompts
- The boundary between them should be explicit and auditable

## Boundaries

- Fails when task boundaries can't be defined at design time — premature separation creates rigid pipelines
- For exploratory/research tasks, autonomous reasoning should have more latitude over flow control
- The Foundry's own Chief→Expert dispatch pattern already follows this — Chiefs orchestrate deterministically, Experts reason autonomously
