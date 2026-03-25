---
name: WAT Framework — Workflows, Agent, Tools separation
description: Three-layer architecture separating SOPs (markdown workflows), coordination (AI agent), and execution (tool scripts). Each layer independently editable. Non-technical people modify the "what" without touching the "how."
domain: ai_and_agents
source: Nate Herk "Build & Sell with Claude Code" (10hr course, 550K subs), AI Automation Society, Skool community posts
confidence: high
date_added: 2026-03-25
date_verified: 2026-03-25
tags: [agent-architecture, workflows, separation-of-concerns, claude-code, automation, sops]
related: [claude_code_skill_architecture.md, agentic_workflows_patterns.md]
---

## Pattern

Separate automation systems into three independent layers: **Workflows** (markdown SOPs defining objectives, inputs, tools, and outputs in a `/workflows` folder), **Agent** (AI coordinator that reads workflows, selects tools, handles failures), and **Tools** (executable scripts that perform actions — API calls, data transformations, in a `/tools` folder).

Each layer is independently editable and testable. Non-technical people can modify workflows (the "what") without touching tools (the "how"). The agent layer is the only part that needs AI capability — workflows and tools are deterministic.

## Evidence

- Nate Herk 10hr Claude Code course: entire course structured around this framework
- Structure: `/workflows` folder with markdown SOPs, `/tools` folder with Python scripts, Claude Code agent as coordinator
- Course requires zero lines of code from the user — the framework makes this possible by separating concerns

## Apply When

- Building any repeatable automation with an AI agent
- When non-technical stakeholders need to modify automation behavior
- When the same tools serve multiple different workflows
- Structuring agent projects for maintainability and handoff

## Boundaries

- Requires discipline to keep workflows as pure SOPs and not leak implementation details into them
- Falls apart if tools aren't well-documented enough for the agent to use them correctly
- Adds overhead for one-off automations — only worth it for repeatable processes
