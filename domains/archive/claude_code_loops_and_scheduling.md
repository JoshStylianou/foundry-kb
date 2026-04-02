---
name: Claude Code Loops and Scheduled Tasks
description: /loop for session-bound recurring prompts, /schedule for persistent daily/weekly automation, cron tools, limitations, Google Workspace CLI
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcript (Nate Herk, "4 Claude Code Updates")
confidence: medium
date_added: 2026-03-24
tags: [scheduling, automation, cron, loops, remote-triggers]
related: [claude_code_advanced_workflows.md]
---

## Two Tiers of Recurring Automation

| | /loop | /schedule (Scheduled Tasks) |
|--|-------|---------------------------|
| **Duration** | Expires after 3 days | Persistent until deleted |
| **Session** | Lives in current session only | Fresh instance each run |
| **Missed runs** | Lost forever — no catch-up | Catches up when app reopens |
| **Availability** | Terminal, VS Code, desktop | Desktop app / Claude Co-work only (as of 2026-03) |
| **Use case** | "Watch this for the next few hours" | "Do this every morning at 9am" |
| **Under the hood** | Cron job in-session | Remote trigger / cron |

## /loop

Fires a prompt or slash command on a recurring interval within the active session.

**Syntax:** `/loop <interval> <prompt or /command>`
- `/loop 10m Check my inbox for important emails`
- `/loop 1d Check my YouTube for new videos and run /content-repurpose`

Can invoke skills by name in the prompt. Also supports one-off reminders: "in one minute remind me to X" → single-fire cron.

**Limitations:**
- Max 3 days
- Session-bound — close terminal = gone
- No catch-up on missed fires
- Think of it as "help me right now" — sprint monitoring, inbox watching, build status polling

## Scheduled Tasks

Persistent automation that survives across sessions. Each fire starts a fresh Claude Code instance, reads project files, runs skills, executes the command, then stops.

**Setup via:** `/schedule` in Claude Code, or "New Task" in Claude Co-work scheduled tasks UI.

**Configuration:** name, description, prompt, frequency (daily/weekly/hourly/custom cron), model, working folder.

**Limitations:**
- Desktop app or Co-work only (not terminal or VS Code extension yet — expect this to change)
- Computer must be on and app open
- Catches up missed runs on reopen

## Cron Tools Under the Hood

Both loops and scheduled tasks use three tools: `CronCreate`, `CronList`, `CronDelete`. Cron = Command Run On Notice — time-based scheduling using cron expressions.

## Google Workspace CLI

Google released an open-source CLI giving Claude Code access to the entire Google ecosystem: Drive, Gmail, Calendar, Docs, Sheets, Slides. 100+ built-in recipes.

**Key advantage over MCP/API approach:** Runs bash commands that talk directly to Google → properly formatted docs with headers, images, links (not raw markdown that needs API calls to format).

**Setup:** Install in terminal or ask Claude Code to set up the Google CLI. Currently in beta ("not officially supported Google product" — but it's Google's own repo).

**Relevance:** Fills the biggest gap in Claude Code's tool ecosystem. Previously only email + calendar via built-in skills. Now full workspace access without complex MCP setup.
