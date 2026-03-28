---
name: Prefill Deprecation on Claude 4.6 — Migration Required
domain: ai_and_agents
tier: reference
confidence: high
source: Anthropic Claude API documentation (platform.claude.com/docs)
created: 2026-03-27
reverify_by: 2026-04-27
---

## Pattern

Claude 4.6 models no longer support prefilled assistant turns on the last message. Any API build using prefills for format forcing, preamble suppression, or continuations must migrate.

## Evidence

Anthropic docs (first-party): "Starting with Claude 4.6 models, prefilled responses on the last assistant turn are no longer supported." Five migration paths documented.

## Decision Rule

- Format-forcing prefills → structured outputs or tool calls with enum fields
- Preamble-suppressing prefills → system prompt instructions ("Respond directly without preamble")
- Continuation prefills → move partial text into user turn
- Context-hydration prefills → tool-based context injection or user-turn reminders
- Audit all Foundry API builds for prefill usage before upgrading models

## Boundaries

- Pre-4.6 models continue to support prefills
- Mid-conversation assistant messages (not the final turn) are unaffected
