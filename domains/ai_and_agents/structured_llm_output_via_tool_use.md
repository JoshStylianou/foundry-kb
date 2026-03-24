---
name: Structured LLM Output via Tool Use
description: Force structured, parseable output from LLMs by using tool_choice with custom tool schemas instead of asking for formatted text
type: pattern
domain: ai_and_agents
source: First-party implementation — Slack EA project (production)
confidence: high
date_added: 2026-03-24
tags: [structured-output, tool-use, llm-patterns, slack, briefing, claude-api]
related: [model_capabilities_map.md]
---

## The Problem

Asking an LLM to "output JSON" or "format as Slack mrkdwn" produces inconsistent results. The model may:
- Add markdown fences around JSON
- Vary field names between runs
- Hallucinate extra fields or omit required ones
- Mix formatting conventions unpredictably

This is especially painful for automated pipelines where the output must be machine-parseable every single time.

## The Pattern: tool_choice with Custom Tool Schemas

Instead of prompting for formatted text, define a **custom tool** whose schema describes the exact output structure you need. Then set `tool_choice` to force the model to "call" that tool — which means it must produce valid JSON matching your schema.

### How It Works

1. **Define a tool schema** that describes your desired output structure (e.g., `submit_brief` with fields for `action_required[]`, `watch[]`, `wins[]`)
2. **Each array item** has typed fields: `channel` (string), `summary` (string), `suggested_message` (string), `priority` (enum)
3. **Set `tool_choice: { type: "tool", name: "submit_brief" }`** in the API call — the model MUST call this tool
4. **Extract the structured data** from `tool_use` content block in the response
5. **Render separately** — a dedicated rendering function converts the structured data into the final format (Slack mrkdwn, HTML, email, etc.)

### Why This Works Better Than Prompting for Format

| Approach | Consistency | Parseability | Post-processing |
|----------|------------|--------------|-----------------|
| "Output as JSON" in prompt | ~80% clean | Fragile — needs regex cleanup | Hard |
| "Use this exact format" in prompt | ~70% clean | Very fragile | Very hard |
| tool_choice with schema | ~99% clean | Guaranteed valid JSON | Trivial — it's already structured |

### Key Benefit: Separation of Content and Presentation

The LLM focuses purely on **what to say** (content, priority, classification). A deterministic rendering function handles **how it looks** (formatting, links, emoji, layout). This separation means:

- You can change the visual format without touching the prompt
- You can post-process the data (e.g., inject clickable Slack channel links via a channelMap lookup)
- You can validate the output programmatically before rendering
- Multiple output formats (Slack, email, dashboard) from the same LLM call

## Model Selection

For high-frequency structured output tasks (10+ calls/day), use a cost-efficient model. In the Slack EA implementation, **claude-sonnet-4-6** handles the structured brief generation — the task is classification and summarisation, not complex reasoning, so Opus-tier models add cost without meaningful quality improvement.

## Where Applied

- **Slack EA project:** `submit_brief` and `submit_leadership_brief` tool schemas produce structured brief data; `renderBrief()` and `renderLeadershipBrief()` convert to Slack mrkdwn

## Pitfalls

1. **Schema complexity ceiling:** Very deeply nested schemas (4+ levels) can confuse the model. Keep schemas flat-ish — arrays of objects with primitive fields work best.
2. **Enum drift:** If you define a priority field as enum `["high", "medium", "low"]`, the model respects it. But if you use free-text fields for things that should be enums, you'll get inconsistent values.
3. **Token overhead:** The tool schema counts toward input tokens. For very large schemas, this adds up on high-frequency calls. Keep schemas tight.
