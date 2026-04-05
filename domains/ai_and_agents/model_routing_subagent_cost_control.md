---
name: Model Routing for Subagent Cost Control
domain: ai_and_agents
tier: reference
confidence: high
source: Anthropic Claude Code documentation (code.claude.com/docs)
created: 2026-03-27
reverify_by: 2026-04-27
---

## Pattern

Route subagent tasks by complexity to control cost. The built-in Explore subagent uses Haiku with read-only tools — this is the reference pattern for cost-effective delegation.

## Evidence

Anthropic's official Claude Code docs (first-party source):
- Built-in Explore subagent uses Haiku with read-only tools (Glob, Grep, Read, WebFetch, WebSearch)
- Model resolution order: (1) CLAUDE_CODE_SUBAGENT_MODEL env var, (2) per-invocation model parameter, (3) subagent definition's model frontmatter, (4) main conversation's model
- The env var override forces ALL subagents to a cheaper model without editing definitions

## Decision Rule

- Exploration and search tasks → Haiku (fast, cheap, read-only)
- Analysis and code review → Sonnet (balanced)
- Complex reasoning or implementation → Opus (or inherit from main)
- Use CLAUDE_CODE_SUBAGENT_MODEL env var for global override during cost-sensitive batch work

## Interface/Engine Decoupling for Cost Routing (April 2026 data)

When the agent interface (what the user interacts with) is separated from the inference engine (what does the reasoning), you can route by task complexity without changing the user experience. Applying maximum-cost infrastructure to minimum-complexity tasks is structural waste.

Price points (April 2026):
- Local Ollama models = $0
- OpenRouter free tier = 29 models at $0 (March 2026)
- DeepSeek V3.2 via OpenRouter = $0.28–$0.42/MTok
- Claude Opus 4.6 = $25/MTok output — 23x difference vs DeepSeek, 96% cheaper

Trade-off: local/cheap models have lower tool-call reliability on complex multi-step chains; Claude models remain most reliable for agentic work.

Source: Nate Herk "How to Use Claude Code 99% Cheaper (2 Methods)" (~Apr 3, 2026)

## Boundaries

- Don't route complex multi-step implementation to Haiku — insufficient reasoning depth
- The env var override is global and affects ALL subagents, which may be too blunt for mixed workloads
- Pricing changes frequently — reverify monthly
- Local/cheap models fail for complex multi-step agentic tasks requiring high tool-call reliability
- Data privacy rules may prevent cloud routing to third-party model providers
