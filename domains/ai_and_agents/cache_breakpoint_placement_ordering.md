---
name: Cache Breakpoint Placement is an Ordering Problem
domain: ai_and_agents
tier: reference
confidence: high
source: Anthropic Claude API documentation (platform.claude.com/docs)
created: 2026-03-27
reverify_by: 2026-04-27
---

## Pattern

Prompt caching delivers 90% cost reduction on cached tokens, but cache hit rates depend on content ordering. Dynamic content before a cache breakpoint invalidates the cache entirely.

## Evidence

Anthropic docs (first-party): "Changes at each level invalidate that level and all subsequent levels." Changing tool_choice invalidates system and messages cache. Anti-pattern: timestamp in a message before a breakpoint causes 100% cache misses. 1-hour cache write costs 2x but persists 12x longer. Batch API + caching stack (50% + 90%).

## Decision Rule

- Most stable content first: tools > system > messages
- Place cache_control on the last block whose prefix is identical across requests
- Never put dynamic content (timestamps, user IDs) before a cache breakpoint
- Longer TTL breakpoints must appear before shorter ones
- Use 1-hour TTL for batch workloads (5-min TTL unreliable with batch processing times)
- Up to 4 breakpoints when sections change at different frequencies

## Boundaries

- Only relevant when using explicit cache breakpoints
- Automatic caching handles placement for simple multi-turn conversations
- JSON key ordering differences between languages (Swift, Go) can break cache matching
