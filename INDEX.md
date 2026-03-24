# The Foundry Knowledge Base — Master Index

**Last updated:** 2026-03-24
**Total entries:** 29
**Active research topics:** 5

---

## How to Use This Index

Agents: read this file before starting any task. Navigate by domain. Do not scan all files — use the index to find what is relevant, then read only those entries.

---

## Domains

| Domain | Description | Entry Count | Last Updated |
|--------|-------------|-------------|--------------|
| [ai_and_agents](domains/ai_and_agents/) | AI models, agent architectures, prompt engineering, Claude API, MCP, automation tools | 23 | 2026-03-24 |
| [growth_marketing](domains/growth_marketing/) | Performance marketing, paid media, conversion, retention, growth frameworks | 0 | — |
| [forex_trading](domains/forex_trading/) | Forex markets, signal logic, risk management, trading frameworks, TraiderJ-specific | 0 | — |
| [business_operations](domains/business_operations/) | Agency ops, team management, SOPs, financial frameworks, AI OS for TNT Growth | 1 | 2026-03-23 |
| [tools_and_software](domains/tools_and_software/) | Specific tools, APIs, integrations — what works, what doesn't, configuration patterns | 4 | 2026-03-24 |
| [meta_learning](domains/meta_learning/) | Knowledge about The Foundry itself — how to run it better, pipeline improvements | 1 | 2026-03-23 |

---

## 5 Most Recent Additions

1. `ai_and_agents/claude_computer_use_and_dispatch.md` — NEW: Claude GUI control as fallback + Dispatch async phone-to-desktop delegation. Research preview, macOS only.
2. `ai_and_agents/claude_api_search_code_execution_ga.md` — NEW: Web search, code execution, structured outputs GA. No beta headers, code execution free with search/fetch.
3. `ai_and_agents/microsoft_agent_framework_replaces_autogen.md` — NEW: AutoGen maintenance mode, replaced by unified Agent Framework SDK (1.0 GA Q1 2026).
4. `ai_and_agents/claude_code_agent_teams.md` — UPDATED: Added key decision rule for when to use teams vs sub-agents (mid-task coordination is the distinguishing factor).
5. `ai_and_agents/structured_llm_output_via_tool_use.md` — Force structured LLM output via tool_choice with custom schemas.

*Also added in this batch (Slack EA production patterns):*
- `ai_and_agents/leadership_domain_sectioned_briefs.md` — Multi-stakeholder briefs with per-domain sections and cross-functional CEO summary
- `tools_and_software/slack_reaction_aware_signal_detection.md` — Emoji reactions from internal team count as acknowledgement, reducing false positive alerts
- `tools_and_software/team_roster_dynamic_loading_with_fallback.md` — API roster loading with hardcoded fallback for internal vs external classification
- `tools_and_software/slack_mrkdwn_clickable_channel_links.md` — channelMap + `<#ID|name>` format for clickable channel references in Slack messages

*Previous additions: `tools_and_software/github_actions_external_cron_scheduling.md`, `ai_and_agents/model_capabilities_map.md`, `ai_and_agents/claude_code_loops_and_scheduling.md`, `ai_and_agents/claude_code_agent_teams.md`, `ai_and_agents/claude_code_skill_architecture.md`, `ai_and_agents/claude_code_self_improving_skills.md`, `meta_learning/pattern-identity-first-agent-design.md`, `ai_and_agents/knowledge_cascade_pattern.md`, `ai_and_agents/consulting_agent_architecture.md`, `ai_and_agents/proactive_ai_advisory_patterns.md`, `ai_and_agents/terminal_ai_multi_model_workflows.md`, `ai_and_agents/claude_code_context_management.md`, `ai_and_agents/agentic_workflows_patterns.md`, `ai_and_agents/claude_code_practical_tips.md`, `ai_and_agents/claude_code_advanced_workflows.md`, `business_operations/selling_agentic_workflows.md`*

---

## Highest Confidence Entries by Domain

All 26 entries currently rated **high confidence** (sourced from structured video transcript analysis, research synthesis, official documentation, and first-party implementation).

---

## Active Research Topics

These topics are monitored daily by the autonomous research loop. Updated by kb-curator after each research cycle.

1. **AI agent architectures and self-improving systems** — tools, frameworks, patterns for building better agent teams
2. **Performance marketing and paid media signals** — relevant to TNT Growth's 60 clients
3. **Forex market signals and AI trading** — relevant to TraiderJ
4. **Claude API and Anthropic updates** — new capabilities, pricing, context limits, tool use patterns
5. **Business AI OS implementations** — how other agencies/firms are implementing AI operations at scale

---

## Tools Built

| Tool | Type | Built | Status |
|------|------|-------|--------|
| [slack-ea-brief](tools_built/slack-ea-brief/) | Claude Code slash command | 2026-03-22 | Deployed, untested in production |
| [slack-ea-github-actions](tools_built/slack-ea-github-actions/) | Node.js + GitHub Actions | 2026-03-22 | Built, ready to deploy |

---

## KB Health

- **Confidence distribution:** 29 high / 0 medium / 0 low / 0 unverified
- **Entries needing verification:** 0
- **Entries due for re-verification:** 0
- **Conflicts flagged:** 0
- **Last autonomous research run:** never
- **Last Josh input ingestion:** 2026-03-24
- **Last confidence audit:** 2026-03-24 (full audit — all citations verified, market data corrected, tool status updated)
