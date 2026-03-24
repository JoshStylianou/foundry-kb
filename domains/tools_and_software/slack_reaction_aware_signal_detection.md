---
name: Slack Reaction-Aware Signal Detection
description: Counting emoji reactions from internal team as acknowledgement to prevent false positive "unanswered message" alerts
type: pattern
domain: tools_and_software
source: First-party implementation — Slack EA project (production)
confidence: high
date_added: 2026-03-24
tags: [slack, signal-detection, false-positives, reactions, emoji, automation, briefing]
related: [../ai_and_agents/precomputed_metadata_for_llm_analysis.md]
---

## The Problem

Automated systems that detect "unanswered client messages" in Slack generate excessive false positives because they only look for text replies. In practice, teams frequently acknowledge messages with emoji reactions (thumbsup, eyes, white_check_mark, heart) without typing a reply. A message with three thumbsup reactions from the internal team is not "unanswered" — it's acknowledged.

Without reaction awareness, every reacted-but-not-replied message triggers a false alert, and users quickly learn to ignore the alerts entirely.

## The Pattern

### Implementation

1. **Define meaningful reaction set** — not all reactions count as acknowledgement:
   ```javascript
   const ACKNOWLEDGEMENT_REACTIONS = [
     'thumbsup', '+1', 'white_check_mark', 'heavy_check_mark',
     'eyes', 'heart', 'raised_hands', 'ok_hand', 'pray'
   ];
   ```

2. **Check reaction authors against internal team roster** — only reactions from internal team members count. A client reacting to their own message is not "acknowledged by the team."

3. **In the unanswered-message detection logic:**
   ```
   message is "unanswered" IF:
     - sent by external user AND
     - no text reply from internal team member AND
     - no meaningful reaction from internal team member
   ```

4. **Feed this as pre-computed metadata** to the LLM (see: pre-computed metadata pattern):
   ```
   [META] #client-acme | unanswered_external: 0 | (1 msg acknowledged via reaction)
   ```

### What Counts as Acknowledged

| Signal | Counts as Acknowledged? |
|--------|------------------------|
| Text reply from internal team member | Yes |
| Meaningful reaction from internal team member | Yes |
| Reaction from external/client user | No |
| Generic reactions (e.g., custom emoji, party) | Depends — define your set |
| Thread reply (not channel reply) | Yes — check both |

## Impact

In the Slack EA project, reaction awareness **reduced false positive "unanswered" alerts by approximately 30-40%** in channels where the team culture favours reaction acknowledgement over typed replies.

## Where Applied

- **Slack EA project:** `computeChannelMetadata()` checks each message's `reactions[]` array for internal user IDs against the team roster

## Pitfalls

1. **Reaction set maintenance:** Teams develop new reaction conventions. Periodically review which reactions your system treats as acknowledgement.
2. **Reaction vs. engagement:** A "eyes" reaction might mean "I've seen this" or "looking into it" — either way, it's acknowledgement. But a "laughing" reaction on a serious client request probably isn't. Be conservative with your reaction set.
3. **API pagination:** Slack's conversations.history returns reactions inline, but conversations.replies may need separate calls for threaded messages. Budget for the API calls.
4. **Rate limiting:** If you're checking reactions across hundreds of channels, batch your Slack API calls carefully to stay within rate limits.
