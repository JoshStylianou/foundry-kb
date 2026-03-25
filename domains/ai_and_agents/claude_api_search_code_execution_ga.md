---
name: Claude API — Web Search, Code Execution, Structured Outputs GA
description: Web search, code execution, and structured outputs are GA on Claude API — no beta headers, code execution free with search/fetch, dynamic filtering pattern
type: insight
domain: ai_and_agents
source: Anthropic release notes + platform changelog, March 2026
confidence: medium
date_added: 2026-03-24
tags: [claude-api, web-search, code-execution, structured-outputs, ga]
related: [model_capabilities_map.md, claude_code_practical_tips.md]
---

## What Changed

As of March 2026, three Claude API features moved from beta to GA:

1. **Web search** — tool_use-based, returns cited results inline
2. **Code execution** — sandboxed Python execution within API calls
3. **Structured outputs** — guaranteed JSON schema conformance via `tool_choice`

No beta headers (`anthropic-beta`) required for any of these. Remove beta headers from existing Foundry apps.

## Code Execution Pricing

Code execution is **free** when used alongside web search or web fetch tools in the same request. This enables a powerful pattern:

**Dynamic filtering:** Run code execution on search/fetch results *before* they hit the context window. The LLM retrieves raw data, code execution filters/transforms it, and only the refined output consumes context tokens. Cuts token cost and noise significantly.

## Operational Impact

- Agent pipelines should filter at the execution layer, not the context layer
- Remove all `anthropic-beta` headers from Foundry trigger code and API calls
- Cost modeling for search-heavy agents improves — code execution adds zero marginal cost when paired with search
- Structured outputs via `tool_choice` with custom schemas is now the recommended path for consistent LLM output (see: structured_llm_output_via_tool_use.md)
