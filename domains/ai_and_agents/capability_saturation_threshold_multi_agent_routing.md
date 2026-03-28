---
title: Capability Saturation Threshold for Multi-Agent Routing
domain: ai_and_agents
tier: core
confidence: high
source: "Google/MIT arXiv:2512.08296 (180 configs, 4 benchmarks, 3 LLM families); InfoQ March 2026"
created: 2026-03-28
last_verified: 2026-03-28
---

## Pattern

Multi-agent coordination harms rather than helps performance once a single-agent system exceeds ~45% task success rate on a given task type. Above this threshold, adding agents produces statistically significant regression (β = −0.408, p < 0.001). Sequential reasoning tasks are uniquely fragile: every multi-agent topology tested degraded performance 39–70% regardless of agent count. Below the threshold, centralized coordination reduces error amplification 3.9× (17.2× → 4.4×) vs. independent agents.

The predictive model achieves 87% accuracy on held-out task domains — meaning architecture selection can be driven by measurable single-agent baseline, not intuition.

## Evidence

Google/MIT "Towards a Science of Scaling Agent Systems" (arXiv:2512.08296). 180 controlled configurations across 4 benchmarks, 3 LLM families (GPT, Gemini, Claude). InfoQ coverage March 2026.

## Apply When

Evaluating whether to add agents to an existing pipeline — measure single-agent baseline first. If >45% success rate, adding agents is statistically more likely to hurt than help. Reserve multi-agent approaches for parallelizable tasks where single-agent baseline is demonstrably low.

## Boundaries

- Benchmark uses well-specified tasks — ambiguous real-world tasks may shift the threshold
- Centralized hub architectures still benefit from error containment even above threshold
- The 45% is a measured inflection point, not a hard ceiling

## Relationship to Other Entries

Complements `multi_agent_orchestration_tax` — that entry covers the cost overhead of multi-agent systems (~3× token/time), this one covers performance regression. Together they form a decision framework: don't add agents if one agent is already good enough (this entry), and even when you do, expect significant overhead (orchestration tax entry).
