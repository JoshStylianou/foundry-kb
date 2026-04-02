---
name: Claude Code Agent Teams — Topology Decision Pattern
description: When to use agent teams vs sub-agents vs worktrees. The distinguishing factor is mid-task communication, not parallelism. Prompt template, context inheritance, dos/don'ts.
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcripts, Anthropic / SitePoint March 2026
confidence: medium-high
date_added: 2026-03-21
date_updated: 2026-04-02
date_verified: 2026-04-02
tags: [agent-teams, multi-agent, claude-code, orchestration, worktrees]
related: [agentic_workflows_patterns.md, multi_agent_orchestration_tax.md]
---

## Three Execution Topologies

| | Sub-Agents | Agent Teams | Worktrees |
|--|-----------|-------------|-----------|
| **Communication** | All through main agent | Shared task list + peer-to-peer | None — full isolation |
| **Coordination** | Hub-and-spoke | Peer-to-peer with shared state | Independent branches |
| **Context at spawn** | Gets only delegated prompt | Gets only spawn prompt (NO conversation history) | Full repo copy |
| **Merge** | Results flow back to main | Agents coordinate live | Manual git merge |
| **Best for** | Simple delegation, sequential | Cross-collaboration, QA loops | Independent features, no conflicts |

## Key Decision Rule

Use **Agent Teams** when agents need to coordinate during execution — sharing discoveries, reacting to each other's output, sending work back for revision mid-task.

Use **Sub-Agents** when you just need independent results reported back at the end.

Use **Worktrees** when features touch different parts of the codebase and must not interfere with each other.

The distinguishing factor is **mid-task communication**, not parallelism.

## Agent Team Prompt Template

1. **Goal** — what the team is building and why (agents wake with zero context)
2. **Team spec** — "Create a team of N teammates using [model]"
3. **Per-agent definition** — role, responsibilities, specific files to own, who to message when done
4. **Inter-agent messaging** — explicit directives: "when done, message QA agent"
5. **Final deliverables** — what the main agent should collect

## Dos and Don'ts

| Do | Don't |
|----|-------|
| Assign each agent specific files to own | Let agents share files (overwrites) |
| Define explicit output/deliverables | Use vague deliverables |
| Name message recipients explicitly | Assume agents know who to talk to |
| Use 3-5 teammates | Go for 10+ (cost = N× single agent) |
| Give full context in spawn prompt | Assume context carries over |

## Context Inheritance

Teammates inherit: permissions, MCP servers, skills, files.
Teammates do NOT inherit: conversation history — fresh start with spawn prompt only.

## Graceful Shutdown

Main agent sends shutdown request. Teammates can **refuse** if not done. Only shut down when teammates confirm they've saved work.
