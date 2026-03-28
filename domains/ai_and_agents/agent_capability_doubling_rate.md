---
name: AI Agent Capability Doubling Rate as Automation Planning Benchmark
domain: ai_and_agents
tier: reference
confidence: medium
source: METR Time Horizon v1.1 (January 2026, 228-task benchmark)
created: 2026-03-27
reverify_by: 2026-06-27
---

## Pattern

AI agent task-completion time horizons are doubling every ~89 days (2024 rate), providing a calibration tool for which workflows to automate now vs defer 3–6 months.

## Evidence

METR Time Horizon v1.1 (January 2026, 228-task benchmark):
- Post-2024 doubling time = 89 days
- Claude Opus 4.5 achieved 50%+ success on tasks requiring ~5 human hours
- Benchmark spans software engineering, research, and operations domains
- Prior doubling rate was ~7 months — significant acceleration

## Decision Rule

- If an agent fails a workflow today, re-evaluate in 90 days before ruling it out permanently
- Set agent autonomy thresholds for long-running tasks at the current 5-hour human-equivalent ceiling
- Use as a planning input for automation roadmaps — what's impossible today may be routine in two quarters

## Boundaries

- Benchmark uses curated, well-specified tasks — ambiguous or novel domain tasks perform materially worse
- 50% success rate ≠ production-grade reliability
- Extrapolation may slow as easy gains compound
- Single benchmark source — no independent replication yet
