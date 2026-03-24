# Slack EA Brief — Tool Spec

**Built:** 2026-03-22
**Type:** Claude Code slash command + instruction set
**Trigger:** `/user:slack-brief`

## What It Does

Scans 50+ TNT Growth Slack channels, detects actionable signals (client escalations, unanswered messages, budget alerts, approvals needed, performance swings, wins), and delivers a formatted executive brief to the #tnt-md-briefs channel or Josh's DMs.

## Architecture

- **Slash command file:** `C:/Users/joshs/.claude/commands/slack-brief.md` — minimal trigger that loads the full instruction set
- **Instruction set:** `C:/Users/joshs/Slack EA/instructions/briefing-agent.md` — comprehensive agent instructions
- **State file:** `C:/Users/joshs/Slack EA/config/state.json` — tracks last run timestamp for incremental scanning
- **Fallback output:** `C:/Users/joshs/Slack EA/output/latest-brief.md` — if Slack posting fails

## Key Components

1. **State management** — Unix timestamp tracking for incremental channel reads
2. **Channel discovery** — Multi-query search with pagination, pattern matching, exclusion list
3. **Message reading** — Batched channel reads with thread expansion for busy threads
4. **Signal detection** — 3-tier priority system (Action Required / Watch / Wins) with conservative classification
5. **Brief formatting** — Slack mrkdwn with copy-paste suggested messages written as Josh
6. **Delivery** — Posts to #tnt-md-briefs or DMs Josh as fallback

## Dependencies

- Slack MCP tools (claude_ai_Slack namespace)
- Claude Code custom slash commands
- File system access for state management
