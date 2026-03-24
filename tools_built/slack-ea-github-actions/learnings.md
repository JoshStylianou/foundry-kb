# Slack EA Brief (GitHub Actions) -- Build Learnings

**Date:** 2026-03-22

## Design Decisions

1. **Stateless over stateful**: Time-based lookback windows are simpler and more reliable than persisting timestamps via GitHub Actions artifacts. Tradeoff: slight overlap between briefs is acceptable.

2. **Batched rate limiting**: Slack rate limits conversations.history at ~50 req/min for internal apps. Batches of 20 with 1.2s delay keeps comfortably under limit even with 100+ channels.

3. **conversations.mark scope**: Requires `channels:manage` / `groups:manage` -- this is more permissive than ideal. If scope is rejected, the mark-as-read step will fail gracefully without affecting the brief.

4. **BST cron alignment**: GitHub Actions cron is UTC-only. Schedule targets BST. Must manually adjust twice a year (March forward, October back). Comment in YAML documents this.

## What to Watch in Production

- First run: verify bot is member of channels it should scan. If the bot isn't added to channels, they won't appear in conversations.list.
- Claude API cost: ~100 channels with messages could produce a large input. Monitor token usage in logs.
- The `claude-sonnet-4-6` model string -- verify this is the correct model ID when deploying.

## V3 Improvements

1. Dynamic BST/GMT detection in the script itself (check current UK offset and adjust lookback accordingly)
2. Thread expansion for client/external channels where last message is from external person
3. Historical signal trending across briefs
4. Reaction-based acknowledgment on the brief message
