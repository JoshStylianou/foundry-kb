---
name: Agentic Workflows Patterns
description: WAT framework, self-healing boundaries, four key shifts from traditional automation, A2A protocol
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcripts
confidence: high
date_added: 2026-03-21
tags: [agentic-workflows, agent-patterns, orchestration, error-handling]
related: [agentic_deployment_patterns.md, claude_code_agent_teams.md]
---

## WAT Framework

| Component | What It Is | Example |
|-----------|-----------|---------|
| **W**orkflows | Markdown SOPs — the process documented as steps | `skill.md` defining a publishing workflow |
| **A**gent | Claude Code (or equivalent) — the executor | Reads the SOP, makes decisions, calls tools |
| **T**ools | Python scripts, APIs, MCP servers — the hands | Script that posts to LinkedIn, fetches analytics |

## The Self-Healing Boundary

**Critical distinction most people miss:**

- Self-healing works **during active sessions** — the agent can detect errors, adjust, retry, and recover in real time.
- Self-healing does **NOT** work after deployment — deployed code runs deterministically like traditional automation. There is no agent in the loop at runtime.

**The real advantage is in the build process:** the agent handles edge cases, error paths, and unexpected inputs *during construction*, producing more robust code than a human would write manually. But once deployed, it's just code.

## Four Key Shifts from Traditional Automation

1. **Self-healing during build** — Agent catches and fixes errors as it constructs the solution
2. **Natural language control** — Describe what you want in words, not code
3. **Security review on every change** — Agent can review its own output for vulnerabilities before committing
4. **Instant API/MCP integration** — New tools and services can be wired in conversationally, not through manual SDK integration

## A2A Protocol

Google's Agent-to-Agent protocol (announced April 2025) enables standardised agent-to-agent communication. Allows agents built on different platforms to discover each other's capabilities and collaborate. Worth monitoring as it matures — potential foundation for cross-platform agent teams.
