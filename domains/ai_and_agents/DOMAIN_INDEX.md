# AI & Agents — Domain Reference Index

Reference-tier entries for this domain. For Core patterns, see the main [INDEX.md](../../INDEX.md).

| Entry | Confidence | One-line |
|-------|-----------|----------|
| [agentic_deployment_patterns](agentic_deployment_patterns.md) | medium | Three waves of agent deployment, market sizing, trigger.dev patterns |
| [async_agent_delegation_via_mcp_event_bridge](async_agent_delegation_via_mcp_event_bridge.md) | medium | MCP bridges decouple agent execution from terminal. Research preview, API will change. |
| [brief_windows_calibrated_by_type](brief_windows_calibrated_by_type.md) | medium-high | Calibrate brief time windows per content type. Slack EA implementation. |
| [channel_tier_classification_for_briefing](channel_tier_classification_for_briefing.md) | medium-high | Classify channels before LLM analysis. Reduces noise, improves signal. |
| [claude_1m_context_flat_pricing](claude_1m_context_flat_pricing.md) | medium-high | Long-context surcharge removed. RAG is now quality decision, not cost decision. |
| [claude_api_search_code_execution_ga](claude_api_search_code_execution_ga.md) | medium | Web search + code execution GA. Feature announcement — may change. |
| [claude_code_advanced_workflows](claude_code_advanced_workflows.md) | medium | GSD/BMAD frameworks, worktrees, AI dev mindset. Star counts will be stale. |
| [claude_code_agent_teams](claude_code_agent_teams.md) | medium-high | Sub-agents vs agent teams distinction. Claude Code-specific architecture. |
| [claude_code_context_management](claude_code_context_management.md) | medium | Context rot patterns, progressive disclosure. YouTube-sourced, not benchmarked. |
| [claude_md_four_pillars_design](claude_md_four_pillars_design.md) | medium-high | Four functions of a claude.md: knowledge compression, preferences, capability declaration, failure log. 45x compression evidence. |
| [dual_loop_system_prompt_improvement](dual_loop_system_prompt_improvement.md) | medium-high | Local loop (per-feature) + global loop (/insights) for continuous system prompt improvement. Probability decay math. |
| [claude_code_loops_and_scheduling](claude_code_loops_and_scheduling.md) | medium | /loop and /schedule features. Feature documentation, will change. |
| [claude_code_practical_tips](claude_code_practical_tips.md) | medium | Collection of tips: hooks vs skills, Gemini fallback, verification tables. |
| [claude_code_skill_architecture](claude_code_skill_architecture.md) | medium-high | Capability uplift vs encoded preference. Six-step framework. Tool-specific. |
| [claude_computer_use_and_dispatch](claude_computer_use_and_dispatch.md) | medium | GUI control + Dispatch. Research preview, macOS only, not production-ready. |
| [five_component_prompt_formula_workflows](five_component_prompt_formula_workflows.md) | medium | Trigger + Source + Ops + Output + Constraints for reliable workflow generation. |
| [google_ai_max_url_to_multichannel](google_ai_max_url_to_multichannel.md) | medium | URL + ROAS = 5-channel campaign. Google-published data, not independently verified. |
| [knowledge_cascade_pattern](knowledge_cascade_pattern.md) | medium | Six-level knowledge hierarchy. Self-referential — Foundry's own architecture. |
| [leadership_domain_sectioned_briefs](leadership_domain_sectioned_briefs.md) | medium-high | Multi-stakeholder briefs with domain sections. Cross-functional summary rule. |
| [mcp_collapses_tool_ui_into_output_format](mcp_collapses_tool_ui_into_output_format.md) | medium | MCP access collapses tool UI to output format. Two YouTube sources, same niche. |
| [microsoft_agent_framework_replaces_autogen](microsoft_agent_framework_replaces_autogen.md) | medium-high | AutoGen in maintenance mode. Verifiable fact + decision rule. |
| [model_capabilities_map](model_capabilities_map.md) | medium | Point-in-time snapshot. Pricing and capabilities will be stale within weeks. |
| [background_memory_consolidation](background_memory_consolidation.md) | medium | Periodic background consolidation prevents agent memory decay. 913 sessions in 9 min. Not GA yet. |
| [classifier_gated_permission_tiers](classifier_gated_permission_tiers.md) | medium-high | Three-tier permission layers for autonomous agents. 0.4% FP, 5.7% FN on exfiltration. |
| [multi_agent_orchestration_tax](multi_agent_orchestration_tax.md) | medium-high | Multi-agent crews impose ~3× token/time overhead on single-step tasks. Route by complexity. |
| [multi_tool_terminal_orchestration](multi_tool_terminal_orchestration.md) | medium | Multiple AI terminals on same project. Session closer agent. OpenCode details. |
| [agent_capability_doubling_rate](agent_capability_doubling_rate.md) | medium | Agent task horizons doubling every ~89 days. Planning calibration tool. |
| [model_routing_subagent_cost_control](model_routing_subagent_cost_control.md) | high | Route subagent tasks by complexity: Haiku for search, Sonnet for analysis, Opus for reasoning. Env var for global override. |
| [mcp_roadmap_aware_architecture](mcp_roadmap_aware_architecture.md) | high | Check MCP roadmap before building infrastructure. Several needed features are actively being built. |
| [anti_prompting_regression_on_newer_models](anti_prompting_regression_on_newer_models.md) | high | Soften aggressive prompt language when upgrading to 4.6 — overtriggering replaces undertriggering. |
| [prefill_deprecation_on_claude_46](prefill_deprecation_on_claude_46.md) | high | Prefilled assistant turns deprecated on 4.6. Migrate to structured outputs or system prompt instructions. |
| [cache_breakpoint_placement_ordering](cache_breakpoint_placement_ordering.md) | high | Cache hit rates depend on content ordering. Dynamic content before breakpoints invalidates cache. |
| [constraint_first_reliability_production_agents](constraint_first_reliability_production_agents.md) | high | Deterministic structural brackets around LLM decisions for production reliability. Stripe Minions: 1,300 PRs/week. |
| [context_window_coordination_budget_subagent_depth](context_window_coordination_budget_subagent_depth.md) | medium-high | Context window = coordination budget. Delegate depth to isolated subagents. Q1 2026 cross-framework convergence. |
| [incremental_permission_escalation_agent_safety](incremental_permission_escalation_agent_safety.md) | medium-high | Trust ladder: calendar read → email read → draft → send. Progressive permission expansion beats broad upfront access. |
| [organizational_hierarchy_multi_agent_coordination](organizational_hierarchy_multi_agent_coordination.md) | medium | Org chart structure as coordination mechanism for multi-agent systems. Paperclip pattern — escalation, budgets, heartbeats. |
