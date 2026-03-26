---
name: Claude Code Agent Teams
description: Agent teams vs sub-agents — architecture, prompt patterns, plan approval, file ownership, shutdown, sizing, dos/don'ts
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcripts
confidence: medium-high
date_added: 2026-03-21
date_updated: 2026-03-24
date_verified: 2026-03-24
source_updated: Anthropic / SitePoint, March 2026
tags: [agent-teams, multi-agent, claude-code, orchestration]
related: [agentic_workflows_patterns.md, claude_code_advanced_workflows.md]
---

## Agent Teams vs Sub-Agents

| | Sub-Agents | Agent Teams |
|--|-----------|-------------|
| **Communication** | All through main agent (delegation bottleneck) | Shared task list + direct inter-teammate communication |
| **Coordination** | Hub-and-spoke | Peer-to-peer with shared state |
| **Context at spawn** | Gets only the delegated prompt | Gets only the prompt from main agent — NO conversation history |
| **Best for** | Simple delegation, sequential, focused results | Cross-collaboration, parallel work, QA review loops |

## Prompt Template

Effective agent team prompts follow this structure:

1. **Goal** — what the team is building and why (agents wake with zero context)
2. **Team spec** — "Create a team of N teammates using [model]"
3. **Per-agent definition** — role, responsibilities, specific files to own, who to message when done
4. **Inter-agent messaging** — explicit directives: "when done, message the QA agent" / "wait for backend dev's message"
5. **Final deliverables** — what the main agent should collect and present

## Key Decision Rule

Use Agent Teams when agents need to **coordinate during execution** — sharing discoveries, reacting to each other's output, sending work back for revision mid-task. Use sub-agents when you just need independent results reported back at the end. The distinguishing factor is mid-task communication, not parallelism.

## When to Use / When Not To

| Use Agent Teams When | Use Sub-Agents Instead |
|---------------------|----------------------|
| Multiple specialised areas in parallel | Sequential process (1→2→3) |
| Agents need to react to each other | Focused, independent result needed |
| QA review loops (agent sends work back) | Agents don't need to communicate |
| High-quality output requiring coordination | Simple tasks, cost-sensitive work |
| | Everything needs to be in one context window |

## Context Inheritance

Teammates inherit from main session:
- **Permissions** (bypass permissions = all agents get bypass)
- **MCP servers, skills, files** — all accessible
- **NOT inherited:** conversation history — they start fresh with only the spawn prompt

## Plan Approval Mode

Teammates can be required to plan before executing. Three options:
1. Main agent approves each teammate's plan (recommended)
2. User manually approves every plan
3. Dedicate one teammate as plan reviewer/approver

## Dos and Don'ts

| Do | Don't |
|----|-------|
| Assign each agent specific files to own | Let agents share files (they overwrite each other) |
| Define explicit output/deliverables | Use vague deliverables |
| Name message recipients explicitly | Assume agents know who to talk to |
| Use 3-5 teammates | Go for 10+ agent swarms (cost = N× single agent) |
| Give full context in spawn prompt | Assume context carries over from conversation |

## Graceful Shutdown

Main agent sends shutdown request to each teammate. Teammates can **refuse** if not done — "I'm not done yet, let me save." Only shut down when teammates confirm they've saved work. Never force-kill mid-task.

## Tmux Split-Pane View

Running in tmux (requires workaround on Windows) lets you:
- See each agent working in real time in separate panes
- Individually message any teammate directly
- Monitor and intervene without going through main session

## Setup

Enable via environment variable in `settings.local.json` (experimental, disabled by default). Copy the JSON from Claude Code docs → agent teams section.
