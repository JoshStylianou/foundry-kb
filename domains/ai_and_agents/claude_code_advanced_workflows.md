---
name: Claude Code Advanced Workflows
description: Worktrees for parallel feature branches, community frameworks (GSD, BMAD), and AI dev mindset patterns
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcript (Chase AI Plus, "15 Claude Code Tips")
confidence: high
date_added: 2026-03-22
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

Frameworks are community-built "mods" that change how Claude Code approaches problems. They layer on top of Claude Code's native behaviour — it's still Claude doing everything, but with modified logic for planning, sub-agent usage, and context management.

**Examples:**
- **GSD (Get Stuff Done)** — Praised for context window management and sub-agent orchestration patterns
- **BMAD** — Alternative framework with its own approach to project structuring

**Assessment:** Frameworks are personal preference. They can help with complex projects but add overhead. Evaluate whether the framework's approach actually improves on Claude Code's native behaviour for your specific workflow before adopting.

## AI Dev Mindset

The gap between "accept monkey" and AI developer is knowing **what to ask**, not knowing the answers. Key prompts to build this skill:

- "What am I not thinking about?"
- "Is this the best way forward?"
- "What would an expert in [domain] do here?"
- "Why did you make that choice?" (after Claude executes)

The goal is understanding the building blocks, not writing the code. Without this, complexity beyond simple apps becomes unmanageable because you can't ask the right questions or nudge Claude in the right direction.
