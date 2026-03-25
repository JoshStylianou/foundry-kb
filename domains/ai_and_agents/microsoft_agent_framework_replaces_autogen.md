---
name: Microsoft Agent Framework Replaces AutoGen
description: AutoGen is in maintenance mode — Microsoft merged it with Semantic Kernel into a unified Agent Framework SDK (1.0 GA Q1 2026)
type: insight
domain: ai_and_agents
source: lumichats.com, Microsoft official announcements, March 2026
confidence: medium-high
date_added: 2026-03-24
tags: [microsoft, autogen, semantic-kernel, agent-framework, deprecated]
related: [agentic_workflows_patterns.md]
---

## Key Facts

- **AutoGen** is now in maintenance mode (bug fixes only, no new features)
- Microsoft merged AutoGen and Semantic Kernel into a single **Agent Framework SDK**
- **1.0 GA: Q1 2026** — Python and .NET
- Adds: OpenTelemetry observability, PII detection, prompt shields

## Foundry Impact

- Any architecture recommendation that references AutoGen for .NET or Azure workloads should be updated to reference the unified Agent Framework instead
- AutoGen remains functional but is a dead-end — do not recommend for new builds
- The observability and safety features (OTel, PII detection, prompt shields) make this relevant for enterprise client recommendations at TNT Growth

## Decision Rule

If someone asks about multi-agent orchestration on Microsoft/.NET stack: recommend the unified Agent Framework SDK, not AutoGen. If they're already on AutoGen, migration path exists but only worth it for active development — maintenance-mode AutoGen still runs.
