---
name: Claude Code Advanced Workflows
description: Worktrees for parallel feature branches, community frameworks (GSD, BMAD), and AI dev mindset patterns
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcript (Chase AI Plus, "15 Claude Code Tips")
confidence: high
date_added: 2026-03-22
date_verified: 2026-03-24
tags: [claude-code, workflows, subagents, hooks, mcp]
related: [claude_code_practical_tips.md, claude_code_agent_teams.md, claude_code_skill_architecture.md]
---

## Worktrees — Parallel Feature Development

Worktrees let you run multiple Claude Code instances on **separate git branches** simultaneously, then merge when done. Unlike agent teams (which share a codebase and communicate), worktrees give each instance full isolation.

**Usage:** `claude --work-tree feature-<name>` in separate terminals.

| | Agent Teams | Worktrees |
|--|-------------|-----------|
| **Isolation** | Shared codebase, shared task list | Separate git branches, full isolation |
| **Communication** | Agents talk to each other | No inter-instance communication |
| **Merge** | Automatic (agents coordinate) | Manual git merge after both complete |
| **Best for** | Interdependent features | Independent features that won't conflict |

**When to use:** Two or more features that touch different parts of the codebase and can be developed independently. E.g., dark mode in one terminal, PDF export in another.

**When not to use:** Features that modify the same files — merge conflicts will be painful.

## Community Frameworks (GSD, BMAD)

Frameworks that layer on top of Claude Code's native behaviour — modified logic for planning, sub-agent usage, and context management. Both have evolved significantly since launch.

**GSD (Get Stuff Done)** — v2 is now a standalone CLI built on the Pi SDK, no longer just prompt injection.
- 31k+ stars (original) + 3k stars (GSD-2), v2.42.0 current
- Manages context windows, sessions, git branches, cost/token tracking, stuck-loop detection, crash recovery
- Supports three runtimes: Claude Code, OpenCode, and Gemini CLI
- Used by engineers at Amazon and Google

**BMAD (Breakthrough Method for Agile AI-Driven Development)** — Full agile methodology, Claude Code-native.
- 42.1k stars, 130 contributors, v6.2.1 (updated March 24, 2026)
- 21 specialised agents, 50+ guided workflows
- v6 adapted to Claude Code's native features with token-usage optimisations
- Migrating from custom workflow.yaml to Claude Code's native SKILL.md format

**Assessment:** Both are serious tools with large communities, not hobby projects. GSD focuses on execution engine (context rot prevention, multi-runtime). BMAD focuses on full development methodology (agile process, agent team orchestration). Evaluate based on whether you need an execution wrapper (GSD) or a methodology framework (BMAD).

## AI Dev Mindset

The gap between "accept monkey" and AI developer is knowing **what to ask**, not knowing the answers. Key prompts to build this skill:

- "What am I not thinking about?"
- "Is this the best way forward?"
- "What would an expert in [domain] do here?"
- "Why did you make that choice?" (after Claude executes)

The goal is understanding the building blocks, not writing the code. Without this, complexity beyond simple apps becomes unmanageable because you can't ask the right questions or nudge Claude in the right direction.
