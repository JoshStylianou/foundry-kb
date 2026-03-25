---
name: Model Capabilities Map
description: Living reference — which LLM/API is best for which specific Foundry task, with verified capabilities, pricing, and integration points
type: insight
domain: ai_and_agents
source: Stark assessment + live API verification (2026-03-24)
confidence: medium
date_added: 2026-03-24
tags: [multi-model, api, perplexity, gemini, claude, model-selection]
related: [terminal_ai_multi_model_workflows.md]
---

## Purpose

The Foundry is model-literate, not model-loyal. This map tracks which LLM is genuinely best for each recurring Foundry task. Entries are added only when a model is provably better — not for coverage.

**Decision rule:** Use Claude for everything unless this map says otherwise for a specific task.

## Capability Map

| Task | Best Tool | Why | Integration Point | Verified |
|------|-----------|-----|-------------------|----------|
| Deep reasoning, synthesis, long-context analysis | Claude Opus 4.6 | Best reasoning, 1M context | Stark, Chiefs, QA gate | Yes |
| Code generation, review, multi-file changes | Claude Sonnet/Opus | Best agentic coding | Builder agents, Claude Code | Yes |
| Orchestration of research/build pipelines | Claude Sonnet 4.6 | Cost-effective for coordination | Daily research trigger, pipeline | Yes |
| Real-time cited web search | Perplexity Sonar | Inline citations with every response; grounded in live web results; citations now free | Daily research trigger — search step | Yes |
| YouTube video content extraction | Gemini 2.5 Flash | Google owns YouTube; native video+audio URL ingestion (not just transcripts); timestamp-aware | Daily research trigger — YouTube URLs | Yes |
| Google Workspace document access | Google Workspace CLI (gws) | Native formatting, 100+ recipes, bash-accessible | Any skill needing Drive/Docs/Sheets | Yes (josh@tntgrowth.com) |

## Integration Architecture

```
Daily Research Trigger (Claude Sonnet — orchestrator)
  ├── Search step → Perplexity API (sonar) via curl → cited results
  ├── YouTube step → Gemini API (2.5-flash) via curl → video summaries
  └── Synthesis step → Claude Sonnet → brief compilation + signal filtering

Local Stark Session
  ├── Perplexity MCP → interactive cited search
  └── Gemini MCP → ad-hoc YouTube video analysis
```

Other models are called as tools, never as orchestrators. Claude stays in control of workflow logic.

## API Reference

### Perplexity — VERIFIED 2026-03-24
- **Endpoint:** `https://api.perplexity.ai/chat/completions` (OpenAI-compatible)
- **Auth:** `Authorization: Bearer pplx-...` (key from perplexity.ai/settings/api)
- **Models:**
  - `sonar` — fast search+Q&A, $1/M input+output tokens, ~1200 tok/s (Llama 3.3 70B base)
  - `sonar-pro` — complex multi-step research, $3/M input, $15/M output
  - `sonar-reasoning-pro` — reasoning+search, $2/M input, $8/M output
  - `sonar-deep-research` — autonomous deep research, $2/M input, $8/M output, $2/M citations
- **Per-request fee:** ~$5/1K requests (sonar, low search context) to ~$22/1K (pro search, high context)
- **Key feature:** Citations array in every response — URLs that grounded each claim. Citation tokens FREE for sonar and sonar-pro (2026 change).
- **Free tier:** None. Pay-as-you-go only. ($5K credits available via Startups program.)
- **Daily research cost estimate:** 5-10 requests/day = ~$0.03-0.05/day

### Gemini — VERIFIED 2026-03-24
- **Endpoint:** `https://generativelanguage.googleapis.com/v1beta/models/{model}:generateContent`
- **Auth:** `?key=AIza...` query param (key from aistudio.google.dev)
- **Models (current):**
  - `gemini-2.5-flash` — 10 RPM, 250 req/day free, $0.15/M input, $0.60/M output (paid)
  - `gemini-2.5-pro` — 5 RPM, 100 req/day free, deep analysis
  - `gemini-3-flash` — latest, 1M context, $0.50/M input, $3/M output
  - `gemini-3.1-pro-preview` — premium, $2/M input, $12/M output
- **YouTube URL processing:** Pass URL as `file_data` part with `mime_type: "video/mp4"`. Processes actual video frames + audio, not just transcript. Max 8h video/day (preview). Up to 2h per video (2M context) or 1h (1M context). Timestamp-aware queries supported.
- **Free tier:** Generous. 250 req/day on Flash, 100 req/day on Pro. No credit card required.
- **Daily research cost estimate:** FREE (well within free tier for a few videos/day)

### Claude — ACTIVE
- **Endpoint:** Anthropic API / Claude Code native
- **Models:** Opus 4.6 (reasoning, 1M), Sonnet 4.6 (balanced, 1M), Haiku 4.5 (fast/cheap)
- **Pricing:** Sonnet $3/$15 per M tokens, Opus $5/$25 per M tokens. **No surcharge for >200K context** as of 2026-03-13 — standard rates apply up to full 1M window. Competitors still charge 2x past 200-272K.
- **Status:** Primary model for all Foundry operations

## When to Add a New Model

Only add to this map when ALL of these are true:
1. The Foundry has a recurring task (not one-off)
2. A non-Claude model is measurably better at that specific task
3. The integration cost (API key, code change) is justified by quality improvement
4. You can verify the capability with a live test

## Update Log

| Date | Change | Verified By |
|------|--------|-------------|
| 2026-03-24 | Initial map created with placeholder data | Stark |
| 2026-03-24 | Perplexity + Gemini verified live — pricing, models, YouTube capability confirmed | Stark + research agents |
| 2026-03-24 | GWS CLI authenticated (josh@tntgrowth.com) — Drive, Gmail, Calendar, Docs, Sheets | Stark |
| 2026-03-24 | All integrations live — local MCP servers + trigger enhanced + APIs tested | Stark |
| 2026-03-24 | Added Claude long-context surcharge removal (2026-03-13) from daily brief signal | Stark |
