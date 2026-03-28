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

## Boundaries

- Don't route complex multi-step implementation to Haiku — insufficient reasoning depth
- The env var override is global and affects ALL subagents, which may be too blunt for mixed workloads
- Pricing changes frequently — reverify monthly
