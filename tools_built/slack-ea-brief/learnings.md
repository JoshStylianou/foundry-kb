# Slack EA Brief — Build Learnings

**Date:** 2026-03-22

## What Worked

- Slash command as thin trigger + separate instruction file is the right pattern. Keeps the command directory clean and allows instruction iteration without touching the command.
- Explicit team member user ID table prevents misclassification of internal vs external messages.
- Conservative signal classification (when in doubt, WATCH not ACTION) is the right default for an MD-level brief — false alarms destroy trust faster than missed signals.

## What to Improve in V2

1. **User ID resolution**: The hardcoded team member table will go stale as TNT hires/loses people. V2 should dynamically resolve TNT team members (e.g., by checking a Slack user group or channel membership of an internal-only channel).

2. **Channel discovery**: The multi-query search approach works but is verbose. If TNT adopts a consistent naming convention, a single prefix search could replace 11 separate queries.

3. **Scheduling**: Currently manual via `/user:slack-brief`. Could be automated with a cron-triggered n8n workflow that invokes Claude Code CLI, or with a scheduled task.

4. **Historical trending**: V2 could compare signal counts across briefs to detect patterns (e.g., "client-acme has been in ACTION REQUIRED 3 of last 5 briefs").

5. **Brief acknowledgment**: No way to know if Josh read the brief. Could add a reaction-based acknowledgment system.

6. **Thread depth**: Currently only expands threads with 5+ replies. Some critical escalations happen in short threads. Consider expanding any thread in a client/external channel where the last message is from an external person.
