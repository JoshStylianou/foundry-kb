---
name: Slack mrkdwn Clickable Channel Links
description: Build a channelMap from API discovery and inject clickable channel references into Slack messages using the <#ID|name> format
type: pattern
domain: tools_and_software
source: First-party implementation — Slack EA project (production)
confidence: high
date_added: 2026-03-24
tags: [slack, mrkdwn, formatting, channel-links, api, automation]
related: [slack_reaction_aware_signal_detection.md]
---

## The Problem

When posting automated messages to Slack that reference channel names, plain text like `#client-acme` is not clickable. Users have to manually search for the channel. In a brief that references 10+ channels, this creates significant friction.

## The Pattern

### Slack's Channel Link Format

Slack renders clickable channel links using the format:
```
<#C0123ABCDEF|channel-name>
```

Where `C0123ABCDEF` is the channel's internal ID and `channel-name` is the display name. When Slack renders this, users see a clickable `#channel-name` link that navigates directly to the channel.

### Implementation

1. **Build a channelMap at startup** from discovered/joined channels:
   ```javascript
   const channelMap = new Map();
   // From conversations.list or your channel discovery logic
   channels.forEach(ch => channelMap.set(ch.name, ch.id));
   ```

2. **Create a helper function:**
   ```javascript
   const chLink = (name) => {
     const id = channelMap.get(name);
     return id ? `<#${id}|${name}>` : `#${name}`;
   };
   ```

3. **Use in the rendering function** — when converting structured LLM output to Slack mrkdwn, replace channel name references with `chLink(channelName)`

### Why the Fallback Matters

The helper returns plain `#channel-name` if the channel ID isn't in the map. This handles:
- Channels the bot hasn't joined
- Channels created after the map was built
- Typos or renamed channels

A graceful fallback means a missing channel ID never breaks the message — it just isn't clickable.

### When to Build the Map

Build the channelMap from the same channel list you use for data collection. If you're already calling `conversations.list` to find channels to analyse, extract the name-to-ID mapping at the same time. No extra API calls needed.

## Where Applied

- **Slack EA project:** `channelMap` built during channel discovery, `chLink()` helper used in `renderBrief()` and `renderLeadershipBrief()`

## Pitfalls

1. **Channel renames:** If a channel is renamed after the map is built, the old name won't resolve. The map is built per-run so this is only an issue within a single execution.
2. **Private channels:** The bot can only map channels it has access to. Private channels it hasn't been invited to won't appear in the map.
3. **Shared channels (Slack Connect):** These have IDs but may behave differently with link formatting. Test with your specific Slack Connect setup.
4. **Don't embed channel links in the LLM prompt/output.** The LLM doesn't know channel IDs. Keep channel names as plain strings in the structured output and convert to links in the rendering layer.
