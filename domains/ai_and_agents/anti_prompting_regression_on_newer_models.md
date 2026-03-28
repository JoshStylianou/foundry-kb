---
name: Anti-Prompting Regression on Newer Models
domain: ai_and_agents
tier: reference
confidence: high
source: Anthropic Claude API documentation (platform.claude.com/docs)
created: 2026-03-27
reverify_by: 2026-04-27
---

## Pattern

When upgrading to Claude 4.6 models, aggressive prompt language written to combat laziness on older models causes overtriggering, excessive subagent spawning, and overengineering. Prompts must be softened during migration.

## Evidence

Anthropic docs (first-party): "If your prompts were designed to reduce undertriggering on tools or skills, these models may now overtrigger." Opus 4.6 has a "strong predilection for subagents" and may spawn them when a grep would suffice. The model also overengineers by creating extra files and unnecessary abstractions.

## Decision Rule

- When migrating prompts from pre-4.5 to 4.6 models, actively remove "CRITICAL: You MUST..." language
- Replace with natural language instructions
- Watch for overtriggering on tool use and excessive subagent spawning
- If building fresh for 4.6, use natural language from the start

## Boundaries

- Only applies when migrating from pre-4.5 prompts
- Fresh prompts written for 4.6 don't need this treatment
