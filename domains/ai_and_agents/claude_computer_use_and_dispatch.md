---
name: Claude Computer Use + Dispatch
description: Claude can autonomously control a Mac GUI as fallback when no API/MCP exists — Dispatch enables phone-to-desktop async task delegation
type: insight
domain: ai_and_agents
source: CNBC, 9to5Mac, claude.com/blog, March 24 2026
confidence: high
date_added: 2026-03-24
tags: [claude, computer-use, dispatch, gui-automation, async-delegation]
related: [agentic_workflows_patterns.md, claude_code_agent_teams.md]
---

## Computer Use

Claude can now autonomously control a Mac desktop: click, type, browse, interact with IDE, manage files, submit PRs, run tests. This is a **fallback layer** — it activates when no MCP server, API connector, or CLI tool exists for the target application.

Falls back to GUI control only when no programmatic path exists. Prefers APIs/MCPs when available.

## Dispatch

Mobile companion app. The workflow:
1. Assign a task from your phone
2. Claude works autonomously on your Mac
3. You return to finished output ready for review

Establishes the **async task-delegation pattern**: human prompt → autonomous execution → human review.

## Current Limitations

- **Research preview** — not production-ready
- **macOS only** — no Windows or Linux
- **Claude Pro/Max subscription required**
- Permission-first model — Claude asks before taking destructive actions

## Architecture Implications

This adds a new layer to the Foundry's agent capability stack:

```
Priority order (highest to lowest):
1. Native API / SDK integration
2. MCP server connector
3. CLI tool
4. Computer Use (GUI fallback) ← NEW
5. Human manual step
```

When designing agent workflows, Computer Use eliminates the "no API available" blocker. But it's slower and less reliable than programmatic paths — use it as genuine fallback, not primary integration.

## When This Matters for The Foundry

- Tools with no API (some ad platforms, legacy internal tools)
- One-off browser tasks that don't justify building an MCP server
- Prototype/exploration phase before investing in proper integration
- NOT for production automation loops — too slow and fragile
