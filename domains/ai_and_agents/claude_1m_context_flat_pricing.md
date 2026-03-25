---
name: Claude 1M context window at flat per-token pricing
description: Long-context surcharge removed on Opus 4.6 and Sonnet 4.6. 200k-1M token requests bill at same rate as small prompts. RAG is now a quality decision, not a cost decision.
domain: ai_and_agents
source: releasebot.io/updates/anthropic/claude, Anthropic docs, Foundry daily brief 2026-03-25
confidence: medium-high
date_added: 2026-03-25
date_verified: 2026-03-25
tags: [claude, pricing, context-window, 1m-context, rag, cost-modeling, anthropic]
related: [claude_api_search_code_execution_ga.md, claude_code_context_management.md]
---

## Pattern

Claude's 1M token context window is now generally available at flat per-token pricing. Previously, requests exceeding 200k tokens incurred a long-context surcharge, which pushed architecture decisions toward RAG-first designs even when full-context loading would have produced better results. That constraint is gone — a 900k token request costs the same per-token as a 9k one.

Prompt caching (90% input cost savings) and Batch API (50% discount) stack on top, making large-context workflows economically viable at scale.

## Apply When

- Designing agent memory architecture — full context loading is now a viable default before reaching for retrieval
- Cost modeling for document-heavy or memory-heavy agent pipelines
- Deciding between RAG vs. full-context for any workflow on Claude

## Boundaries

- Context window size doesn't change model attention quality — very long contexts may still benefit from structured retrieval for precision-critical tasks
- Prompt caching requires cache-friendly prompt structure (stable system prompts, ordered context)

## What Changed

RAG is now a **quality** decision, not a **cost** decision. Default to full-context loading unless retrieval demonstrably improves output quality for the specific task.
