---
name: Agentic Workflows Patterns
description: WAT framework, self-healing boundaries, four key shifts from traditional automation, A2A protocol
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcripts
confidence: medium-high
date_added: 2026-03-21
date_verified: 2026-03-24
tags: [agentic-workflows, agent-patterns, orchestration, error-handling]
related: [agentic_deployment_patterns.md, claude_code_agent_teams.md]
---

## WAT Framework (Workflows-Agent-Tools)

| Component | What It Is | Example |
|-----------|-----------|---------|
| **W**orkflows | Markdown SOPs in `/workflows` folder — objectives, inputs, tools, outputs | `skill.md` defining a publishing workflow |
| **A**gent | Claude Code (or equivalent) — reads SOPs, selects tools, handles failures | Reads the SOP, makes decisions, calls tools |
| **T**ools | Python scripts in `/tools` folder, APIs, MCP servers | Script that posts to LinkedIn, fetches analytics |

Each layer is independently editable and testable. Non-technical people can modify workflows (the "what") without touching tools (the "how"). The agent layer is the only part requiring AI capability — workflows and tools are deterministic. (Source: Nate Herk 10hr Claude Code course — entire course structured around WAT framework, requires zero lines of code from user.)

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

Google's Agent-to-Agent protocol. Announced April 2025 with 50+ partners (Salesforce, SAP, ServiceNow, PayPal). Contributed to the Linux Foundation June 2025 for vendor-neutral governance. **GA v1.0.0 released March 12, 2026.**

- SDKs: Python, Go, JavaScript, Java, .NET
- 22.8k GitHub stars, 146 contributors
- Enables standardised agent-to-agent communication across platforms — agents discover each other's capabilities and collaborate regardless of framework

**Status:** No longer speculative. This is an emerging industry standard with real adoption. Relevant when designing cross-platform agent architectures or recommending interoperability patterns to clients.
