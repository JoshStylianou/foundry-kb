---
name: Multi-Agent Orchestration Tax
domain: ai_and_agents
tier: reference
confidence: medium-high
source: LangChain State of Agent Engineering benchmark (March 2026)
created: 2026-03-27
reverify_by: 2026-06-27
---

## Pattern

Collaborative multi-agent frameworks impose a measurable "orchestration tax" vs single-agent approaches. When tasks are simple or single-step, the coordination overhead of role-based agent crews consumes significantly more compute than routing to a single capable agent.

## Evidence

LangChain State of Agent Engineering (1,300 respondents, 5 tasks, 2,000 benchmark runs, March 2026):
- CrewAI consumed ~3× the tokens and took ~3× longer than LangChain for identical single-step tasks
- AutoGen slightly above LangGraph/LangChain
- LangChain most token-efficient
- CrewAI powers 12M+ daily agent executions across complex workflows where verification overhead pays off

## Decision Rule

- Single-step or low-verification tasks → single agent or chained calls
- Reserve multi-agent crews for completeness-critical tasks (audits, multi-perspective synthesis, iterative refinement)
- The overhead reverses on genuinely complex multi-step tasks where planning loop cost amortizes

## Boundaries

- Benchmark is LangChain's own — potential bias toward their framework
- Token/time overhead varies by task complexity; the 3× figure is for single-step tasks specifically
- CrewAI's overhead may be worth it for tasks requiring cross-checking or role separation
