---
name: Async agent delegation via MCP event bridge
description: Persistent AI agent sessions accessible from any messaging channel via MCP bridge plugins. Phone instruction → agent picks up task with full local context → replies to same channel. Decouples execution from terminal presence.
domain: ai_and_agents
source: VentureBeat, techbuddies.io, marketingagent.blog, Foundry daily brief 2026-03-25
confidence: medium
date_added: 2026-03-25
date_verified: 2026-03-25
tags: [mcp, async-delegation, channels, telegram, discord, persistent-sessions, remote-work]
related: [claude_computer_use_and_dispatch.md, agentic_workflows_patterns.md]
---

## Pattern

Persistent AI agent sessions can be made accessible from any messaging channel by routing trigger events through MCP bridge plugins. The pattern: phone instruction → agent picks up task with full local context (filesystem, git, APIs) → replies to same channel. This decouples long-running execution from synchronous terminal presence.

Claude Code Channels launched March 20, 2026 as an official Anthropic research preview on Pro/Max accounts. Working bridges exist for Telegram and Discord. All built on MCP as the protocol layer.

This is the broader pattern that Claude Computer Use + Dispatch is one instance of. Dispatch is phone-to-Mac; MCP event bridges generalize this to any-channel-to-any-persistent-session.

## Apply When

- Agent tasks run >5 minutes and don't require real-time human input
- Team needs to delegate work remotely (not sitting at the terminal)
- Building async workflows where trigger → execution → notification spans different interfaces
- Designing multi-agent systems where agents need to be invoked from external events

## Boundaries

- Requires a persistent host machine running the Claude Code session
- MCP plugin allowlist restricts self-hosted customization during research preview
- API contract expected to change Q2–Q3 2026 — don't build production dependencies on current interface
- Claude Code Channels is research preview, Pro/Max only

## What Changed

Agent delegation is no longer bound to the terminal. The async pattern (trigger from anywhere → execute with full context → respond to origin) is now a first-class capability, not a hack.
