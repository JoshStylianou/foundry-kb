# AI & Agents — Domain Reference Index

Reference-tier entries for this domain. For Core patterns, see the main [INDEX.md](../../INDEX.md).

---

### Agent Architecture & Orchestration
| Entry | Confidence | One-line |
|-------|-----------|----------|
| [agentic_deployment_patterns](agentic_deployment_patterns.md) | medium | Three waves of agent deployment, market sizing, trigger.dev patterns |
| [agentic_workflows_patterns](../../INDEX.md) | *(Core)* | WAT framework, self-healing boundaries, four key shifts |
| [consulting_agent_architecture](../../INDEX.md) | *(Core)* | Six-component consulting agent protocol, three-layer cognitive architecture |
| [organizational_hierarchy_multi_agent_coordination](organizational_hierarchy_multi_agent_coordination.md) | medium | Org chart structure as coordination mechanism. Paperclip pattern. |

### Agent Safety & Reliability
| Entry | Confidence | One-line |
|-------|-----------|----------|
| [classifier_gated_permission_tiers](classifier_gated_permission_tiers.md) | medium-high | Three-tier permission layers for autonomous agents. 0.4% FP, 5.7% FN. |
| [constraint_first_reliability_production_agents](constraint_first_reliability_production_agents.md) | high | Deterministic brackets around LLM decisions. Stripe Minions: 1,300 PRs/week. |
| [incremental_permission_escalation_agent_safety](incremental_permission_escalation_agent_safety.md) | medium-high | Trust ladder: read → draft → send. Progressive permission expansion. |

### Multi-Agent Scaling & Coordination
| Entry | Confidence | One-line |
|-------|-----------|----------|
| [capability_saturation_threshold_multi_agent_routing](../../INDEX.md) | *(Core)* | Single-agent >45% = adding agents hurts. 180 configs, 3 LLM families. |
| [multi_agent_orchestration_tax](multi_agent_orchestration_tax.md) | medium-high | Multi-agent crews impose ~3× token/time overhead on single-step tasks. |
| [context_window_coordination_budget_subagent_depth](context_window_coordination_budget_subagent_depth.md) | medium-high | Context window = coordination budget. Delegate depth to subagents. |

### Claude Platform (Code, API, Skills)
| Entry | Confidence | One-line |
|-------|-----------|----------|
| [claude_code_agent_teams](claude_code_agent_teams.md) | medium-high | Agent teams vs sub-agents vs worktrees. Mid-task communication is the decision factor. |
| [claude_code_context_management](claude_code_context_management.md) | medium | Context is milk. Progressive disclosure, context rot at 50-60%, compression. |
| [claude_code_skill_system](claude_code_skill_system.md) | medium-high | Skill types, build framework, binary assertion evals, auto-research loops. |
| [claude_md_four_pillars_design](claude_md_four_pillars_design.md) | medium-high | Four functions of a claude.md: knowledge compression, preferences, capability, failure log. |
| [dual_loop_system_prompt_improvement](dual_loop_system_prompt_improvement.md) | medium-high | Local + global loops for continuous system prompt improvement. |

### Claude API & Model-Specific
| Entry | Confidence | One-line |
|-------|-----------|----------|
| [anti_prompting_regression_on_newer_models](anti_prompting_regression_on_newer_models.md) | high | Soften aggressive prompt language on 4.6 — overtriggering replaces undertriggering. |
| [cache_breakpoint_placement_ordering](cache_breakpoint_placement_ordering.md) | high | Cache hits depend on content ordering. Dynamic before breakpoints invalidates. |
| [claude_1m_context_flat_pricing](claude_1m_context_flat_pricing.md) | medium-high | Long-context surcharge removed. RAG is now quality decision, not cost. |
| [claude_api_search_code_execution_ga](claude_api_search_code_execution_ga.md) | medium | Web search + code execution GA. |
| [model_capabilities_map](model_capabilities_map.md) | medium | Point-in-time snapshot. Pricing will be stale — verify before citing. |
| [model_routing_subagent_cost_control](model_routing_subagent_cost_control.md) | high | Route subagents by complexity: Haiku search, Sonnet analysis, Opus reasoning. |
| [prefill_deprecation_on_claude_46](prefill_deprecation_on_claude_46.md) | high | Prefilled assistant turns deprecated on 4.6. |

### MCP & Tool Integration
| Entry | Confidence | One-line |
|-------|-----------|----------|
| [async_agent_delegation_via_mcp_event_bridge](async_agent_delegation_via_mcp_event_bridge.md) | medium | MCP bridges decouple agent execution from terminal. API will change. |
| [mcp_collapses_tool_ui_into_output_format](mcp_collapses_tool_ui_into_output_format.md) | medium | MCP access collapses tool UI to output format. |
| [mcp_roadmap_aware_architecture](mcp_roadmap_aware_architecture.md) | high | Check MCP roadmap before building infrastructure. |
| [multi_tool_terminal_orchestration](multi_tool_terminal_orchestration.md) | medium | Multiple AI terminals on same project. Session closer agent. |

### Briefing & Advisory Systems
| Entry | Confidence | One-line |
|-------|-----------|----------|
| [brief_windows_calibrated_by_type](brief_windows_calibrated_by_type.md) | medium-high | Calibrate brief time windows per content type. |
| [channel_tier_classification_for_briefing](channel_tier_classification_for_briefing.md) | medium-high | Classify channels before LLM analysis. Reduces noise. |
| [leadership_domain_sectioned_briefs](leadership_domain_sectioned_briefs.md) | medium-high | Multi-stakeholder briefs with domain sections. |
| [watch_item_escalation_across_brief_cycles](../../INDEX.md) | *(Core)* | Inject prior state for temporal reasoning. Escalation across cycles. |

### General AI Patterns
| Entry | Confidence | One-line |
|-------|-----------|----------|
| [agent_capability_doubling_rate](agent_capability_doubling_rate.md) | medium | Task horizons doubling every ~89 days. Planning calibration tool. |
| [background_memory_consolidation](background_memory_consolidation.md) | medium | Periodic background consolidation prevents agent memory decay. Not GA yet. |
| [claude_computer_use_and_dispatch](claude_computer_use_and_dispatch.md) | medium | GUI control + Dispatch. Research preview, macOS only. |
| [five_component_prompt_formula_workflows](five_component_prompt_formula_workflows.md) | medium | Trigger + Source + Ops + Output + Constraints for workflow generation. |
| [knowledge_cascade_pattern](knowledge_cascade_pattern.md) | medium | Six-level knowledge hierarchy. Foundry's own architecture. |
| [microsoft_agent_framework_replaces_autogen](microsoft_agent_framework_replaces_autogen.md) | medium-high | AutoGen in maintenance mode. |
