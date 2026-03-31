# The Foundry Knowledge Base — Master Index

**Last updated:** 2026-03-31
**Total entries:** 63 active (16 Core + 47 Reference) | 2 archived
**Active research topics:** 5

---

## How This Index Works

**Two-tier architecture:**
- **Core** — Transferable principles proven across multiple contexts. Listed below. Always visible to agents.
- **Reference** — Valid but situational knowledge. Listed in each domain's `DOMAIN_INDEX.md`. Agents load these only when working in that domain.

**Promotion/demotion:** Reference entries pulled 3+ times across projects promote to Core. Core entries unreferenced for 60 days get reviewed for demotion.

---

## Core Patterns (16 entries)

These are the highest-value, most transferable patterns in the KB. Every agent should know these exist.

| Entry | Confidence | Domain | Pattern |
|-------|-----------|--------|---------|
| [augmentation_layers_outperform_replacements](domains/ai_and_agents/augmentation_layers_outperform_replacements.md) | high | ai_and_agents | AI layers on existing systems beat full replacements — 23% better CPA at 91% reach across 892 accounts |
| [precomputed_metadata_for_llm_analysis](domains/ai_and_agents/precomputed_metadata_for_llm_analysis.md) | high | ai_and_agents | Pre-compute what LLMs can't do (math, counts, dates) before sending to context. Division of labour between compute and reasoning. |
| [proactive_ai_advisory_patterns](domains/ai_and_agents/proactive_ai_advisory_patterns.md) | high | ai_and_agents | Three-tier proactive model backed by research — 52% engagement, 62% dismissal rates. Competence threat is real. |
| [structured_llm_output_via_tool_use](domains/ai_and_agents/structured_llm_output_via_tool_use.md) | high | ai_and_agents | tool_choice forces structured output at ~99% consistency vs ~80% for plain prompting. Separate content from presentation. |
| [github_actions_external_cron_scheduling](domains/tools_and_software/github_actions_external_cron_scheduling.md) | high | tools_and_software | External cron triggers for unreliable built-in schedulers. First-party production-proven pattern. |
| [agentic_workflows_patterns](domains/ai_and_agents/agentic_workflows_patterns.md) | medium-high | ai_and_agents | WAT framework, self-healing boundaries, four key shifts from traditional automation, A2A protocol |
| [claude_code_self_improving_skills](domains/ai_and_agents/claude_code_self_improving_skills.md) | medium-high | ai_and_agents | Karpathy auto-research loop applied to skills. Binary assertions > subjective scoring for iteration. |
| [consulting_agent_architecture](domains/ai_and_agents/consulting_agent_architecture.md) | medium-high | ai_and_agents | Six-component consulting agent protocol. Consulting vs task agent distinction. Three-layer cognitive architecture. |
| [meta_andromeda_creative_is_targeting](domains/ai_and_agents/meta_andromeda_creative_is_targeting.md) | medium-high | ai_and_agents | Entity ID fingerprinting: conceptual creative diversity IS the targeting mechanism. Rewrites ad account structure. |
| [skills_layer_makes_mcp_reliable](domains/ai_and_agents/skills_layer_makes_mcp_reliable.md) | medium-high | ai_and_agents | Raw MCP insufficient; structured skills layer makes integration production-reliable. 45min→3min with zero errors. |
| [watch_item_escalation_across_brief_cycles](domains/ai_and_agents/watch_item_escalation_across_brief_cycles.md) | medium-high | ai_and_agents | Inject prior state as LLM context for temporal reasoning. Escalation logic across cycles. |
| [shift_based_handoff_for_sustained_autonomous_work](domains/ai_and_agents/shift_based_handoff_for_sustained_autonomous_work.md) | medium | ai_and_agents | Bounded shifts with handoff artifacts > continuous operation. Agents degrade over sustained work. |
| [attribution_reclassification_mimics_performance_decline](domains/growth_marketing/attribution_reclassification_mimics_performance_decline.md) | high | growth_marketing | Platform attribution redefinitions mimic performance drops. Meta March 2026: ~30-40% reported click drop, zero actual change. |
| [pattern-identity-first-agent-design](domains/meta_learning/pattern-identity-first-agent-design.md) | medium-high | meta_learning | Identity-first vs capability-first agent design. Kennedy framework. Identity shapes tool selection. |
| [capability_saturation_threshold_multi_agent_routing](domains/ai_and_agents/capability_saturation_threshold_multi_agent_routing.md) | high | ai_and_agents | Single-agent >45% success = adding agents hurts. Google/MIT, 180 configs, 3 LLM families. Sequential tasks degrade 39-70%. |
| [conversion_signal_floor_algorithmic_delivery](domains/growth_marketing/conversion_signal_floor_algorithmic_delivery.md) | high | growth_marketing | Below 50 weekly conversion events per ad set, CPMs spike 15-40%. Data starvation penalty, not creative failure. |

---

## Domain Reference Libraries

For situational, tool-specific, or project-specific knowledge, see each domain's index:

| Domain | Reference Entries | Last Updated | Index |
|--------|------------------|--------------|-------|
| [ai_and_agents](domains/ai_and_agents/) | 33 | 2026-03-31 | [DOMAIN_INDEX.md](domains/ai_and_agents/DOMAIN_INDEX.md) |
| [business_operations](domains/business_operations/) | 4 | 2026-03-25 | [DOMAIN_INDEX.md](domains/business_operations/DOMAIN_INDEX.md) |
| [tools_and_software](domains/tools_and_software/) | 4 | 2026-03-31 | [DOMAIN_INDEX.md](domains/tools_and_software/DOMAIN_INDEX.md) |
| [security](domains/security/) | 6 | 2026-03-26 | [DOMAIN_INDEX.md](domains/security/DOMAIN_INDEX.md) |
| [growth_marketing](domains/growth_marketing/) | 0 | 2026-03-26 | [DOMAIN_INDEX.md](domains/growth_marketing/DOMAIN_INDEX.md) |
| [meta_learning](domains/meta_learning/) | 0 | 2026-03-26 | [DOMAIN_INDEX.md](domains/meta_learning/DOMAIN_INDEX.md) |
| [forex_trading](domains/forex_trading/) | 0 | — | — |

---

## Confidence Scale

| Rating | Meaning | Count |
|--------|---------|-------|
| **high** | Multiple independent sources, quantified evidence, verified current | 21 |
| **medium-high** | Solid evidence, single source or landscape may have shifted | 18 |
| **medium** | Logical with some evidence, not rigorously quantified | 20 |
| **low-medium** | Thin evidence or single anecdote | 1 |

---

## Active Research Topics

1. **AI agent architectures and self-improving systems**
2. **Performance marketing and paid media signals** (TNT Growth)
3. **Forex market signals and AI trading** (TraiderJ)
4. **Claude API and Anthropic updates**
5. **Business AI OS implementations**

---

## KB Health

- **Confidence distribution:** 21 high / 18 medium-high / 20 medium / 1 low-medium
- **Archived entries:** 2 (domains/archive/)
- **Last confidence audit:** 2026-03-25 (full audit — all 43 entries reassessed, 2 archived, 2 merged)
- **Last Josh input ingestion:** 2026-03-31
