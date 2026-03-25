---
name: Five-component prompt formula for reliable workflow generation
description: Reliable AI-generated workflows require five explicit components in the prompt — Trigger, Data Source, Operations, Output Destination, Constraints. Vague prompts produce unreliable results.
domain: ai_and_agents
source: roborhythms.com, Nate Herk, n8n community demonstrations
confidence: medium
date_added: 2026-03-25
date_verified: 2026-03-25
tags: [prompt-engineering, workflows, automation, reliability, n8n, mcp]
related: [skills_layer_makes_mcp_reliable.md, mcp_collapses_tool_ui_into_output_format.md]
---

## Pattern

When prompting AI to generate automation workflows, include five explicit components for reliable results:

1. **Trigger** — mechanism and frequency (webhook, cron, event)
2. **Data Source** — where input comes from (API, database, file, scrape)
3. **Operations** — transformations, filtering, enrichment steps
4. **Output Destination** — where results go (database, API, notification, file)
5. **Constraints** — error handling, deduplication, format requirements, rate limits

Vague prompts ("monitor Reddit and save leads") produce unreliable workflows. Specific prompts ("Build a workflow that triggers every 4 hours, searches r/n8n for posts with >10 upvotes, extracts title/URL/author, deduplicates against existing entries, and appends to a Google Sheet") produce production-ready output.

## Evidence

- roborhythms.com: documented before/after comparison showing specific prompts dramatically outperform vague ones
- Confirmed across multiple n8n + Claude Code demonstrations
- Known failure patterns when components are missing: webhook auth misconfiguration, complex branching errors (3+ IF/Switch paths), happy-path-only builds (no error handling unless explicitly prompted), default credential selection in multi-credential scenarios

## Apply When

- Every time you prompt an AI to build an automation workflow
- Should be encoded as a skill template or checklist
- Applies beyond n8n — any workflow generation tool (Make, Zapier, custom code)

## Boundaries

- Does not eliminate the four documented failure patterns (webhook auth, complex branching, error handling, multi-credential) — those still need explicit attention or manual verification
- Diminishing returns on very simple workflows (single trigger → single action)
