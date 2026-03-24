# Slack EA Brief (GitHub Actions) -- Tool Spec

**Built:** 2026-03-22
**Type:** Node.js script + GitHub Actions scheduled workflow
**Location:** `C:/Users/joshs/Slack EA/`

## What It Does

V2 of the Slack Executive Assistant. Runs autonomously on GitHub Actions cron (7am, 12pm, 4pm UK weekdays). Scans all TNT Growth Slack channels, sends messages to Claude for signal detection, posts formatted MD brief to #tnt-md-briefs with DM fallback to Josh.

## Architecture

- **Trigger:** GitHub Actions cron schedule (BST-aligned) + manual workflow_dispatch
- **Runtime:** Node.js 20 on ubuntu-latest, 5-minute timeout
- **Slack API:** @slack/web-api -- conversations.list, conversations.history, chat.postMessage, conversations.mark
- **AI:** @anthropic-ai/sdk -- claude-sonnet-4-6 for signal detection and brief generation
- **State:** Stateless -- uses time-based lookback windows (15h morning, 5h midday, 4h EOD)

## Key Components

| File | Purpose |
|------|---------|
| `src/index.js` | Orchestrator -- 5-step pipeline |
| `src/slack.js` | All Slack API calls with rate limiting (batches of 20, 1.2s delay) |
| `src/analyzer.js` | Claude API call with full signal detection prompt |
| `src/formatter.js` | Message formatting for Claude input |
| `src/config.js` | Team roster, channel tiers, exclusions, lookback windows, system prompt |
| `.github/workflows/slack-brief.yml` | Cron schedule, secret injection, brief type detection |

## Secrets Required

SLACK_BOT_TOKEN, ANTHROPIC_API_KEY, SLACK_BRIEF_CHANNEL, JOSH_USER_ID
