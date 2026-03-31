---
name: Four Pillars of Claude.md Design
description: Framework for what a system prompt IS — knowledge compression, preferences, capability declaration, failure log — with 45x compression evidence and solution space pruning
type: insight
domain: ai_and_agents
source: Nick Saraev — "Definitive Claude Code Course for Advanced Users" (YouTube, ~2026)
confidence: medium-high
date_added: 2026-03-29
date_verified: 2026-03-29
tags: [claude-md, system-prompts, prompt-design, token-efficiency, agency]
related: [claude_code_context_management.md, claude_code_self_improving_skills.md]
---

## The Pattern: Four Functions of a System Prompt

A claude.md serves exactly four purposes. Each should be present; none should dominate.

### 1. Knowledge Compression

Compressed summary of the workspace so Claude doesn't re-read every file on every query. The goal is a bird's-eye map, not comprehensive documentation.

**Evidence:** A single-component React app (app.jsx) was ~827 words / ~1,100 tokens. The claude.md summary of the same structure: ~22 words. That's a **45x compression ratio**. Multiply across an entire workspace and the savings are massive — both in cost and in reasoning quality (more tokens in context = lower output quality).

Use `/init` to generate the first pass, then curate.

### 2. Preferences and Conventions

User-specific rules that aren't baked into Claude's defaults. Claude Code natively improves its defaults over time, but advanced users will always have preferences that outpace native support.

Examples: "always return clickable absolute file paths," "use functional programming in Rust," "read API docs before attempting integration — never guess."

**Global vs local split:** Global preferences (response style, time-vs-money tradeoffs, programming paradigm) go in `~/.claude/CLAUDE.md`. Project-specific conventions go in the project's `.claude/CLAUDE.md`.

### 3. Capability Declaration

Claude consistently underestimates its own agency. Without explicit capability statements, it will:
- Give 3-month estimates for tasks it can complete in seconds
- Offer CLI commands for the user to run instead of running them itself
- Say "I don't have a built-in way to do this" when the capability exists via skills/MCP/tools

**Fix:** Explicitly enumerate what Claude can do. "You can call this API. You can browse with MCP. You can run autonomous 15-minute plans. You can execute, not just suggest."

This is the most underrated section. Agency doesn't emerge from intelligence alone — it requires the agent to *know* it has agency.

### 4. Failure and Success Log ("Lab Notes")

A running log of what worked and what didn't, maintained across sessions.

**Mental model — solution space pruning:** If the total space of possible actions Claude could take is a circle, the failure log carves out ~80% of it as "already tried, doesn't work." This forces Claude to focus tokens and reasoning on the remaining 20% that actually matters.

**Implementation:** Add a meta-instruction: "When you make a mistake, update claude.md with what not to try next time." This creates a self-improving system prompt without manual effort.

**Compounding effect:** First loop takes X time. Second loop: 0.9X. Third: 0.8X. The improvement asymptotes but the early gains are dramatic.

## Application Trigger

When designing or auditing any claude.md (global or project), check all four pillars are present. Most claude.mds over-index on #2 (preferences) and completely miss #3 (capability declaration) and #4 (failure log).

## Boundaries

- This is a design framework, not a template. The specific content varies wildly by project.
- Don't over-stuff any pillar. Token cost of the system prompt itself matters (see: context_management entry).
- The failure log needs periodic pruning or it becomes context bloat. Keep only learnings that changed behaviour.
