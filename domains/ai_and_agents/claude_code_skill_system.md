---
name: Claude Code Skill System — Architecture, Iteration, and Self-Improvement
description: Skill types (capability uplift vs encoded preference), six-step build framework, binary assertion evals, auto-research loops, hooks vs skills vs commands. The complete pattern for building and iterating production-quality skills.
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcripts, Anthropic docs
confidence: medium-high
date_added: 2026-03-21
date_updated: 2026-04-02
date_verified: 2026-04-02
tags: [skills, claude-code, architecture, evals, self-improving, assertions]
related: [claude_code_context_management.md, claude_code_agent_teams.md]
---

## Two Types of Skills

| Type | Definition | Durability | Example |
|------|-----------|------------|---------|
| **Capability uplift** | Prompts that teach Claude to do something better | Fades as models improve | "Write concisely", "Use structured output" |
| **Encoded preference** | Sequential workflows specific to your business | Stays durable — model can never guess your process | "Publish to LinkedIn with our tone, formatting, and CTA pattern" |

**Implication:** Invest build time in encoded preference skills. Capability uplift skills are temporary scaffolding.

## Six-Step Build Framework

1. **Name & trigger** — what it's called + natural language that fires it
2. **Goal** — one sentence: what will this skill accomplish?
3. **Step-by-step process** — if you did this manually, what do you do, in what order?
4. **Reference files** — what context is needed? Brand voice, style guides, API docs
5. **Rules/guardrails** — what could go wrong? Build in constraints
6. **Self-improvement loop** — test, iterate, watch the agent work, give feedback

## Hooks vs Skills vs Slash Commands

| Mechanism | Trigger | Token Cost | Best For |
|-----------|---------|------------|----------|
| **Slash commands** | Manual (`/command`) | Minimal | Quick actions user explicitly invokes |
| **Skills** | Auto-triggered by description match | Medium-high | Complex workflows that should activate automatically |
| **Hooks** | Programmatic (settings.json) | Zero LLM tokens | Guardrails, format enforcement — anything rule-based |

**Key insight:** Hooks run without consuming LLM tokens. Use hooks for deterministic rules (regex, word lists). Reserve skills for things requiring judgment.

## File Structure

```
.claude/skills/skill-name/
├── skill.md          # Process/SOP (under 500 lines)
├── references/       # Knowledge loaded on demand
├── scripts/          # Executable code
└── assets/           # Templates, examples, sample outputs
```

## Progressive Context Loading

| Tier | What | When | Token Cost |
|------|------|------|------------|
| 1 | YAML front matter | Every request (scans all skills) | ~100 tokens |
| 2 | Full skill.md body | On skill activation | 1,000–2,000 tokens |
| 3 | References, scripts, assets | When a specific step needs them | Variable |

Skill descriptions must be precise — Tier 1 is the filter. ~20% activation with vague descriptions, ~84% with optimized keywords.

## Self-Improving Skills — The Auto-Research Loop

`make a change → run test → check score → keep or revert → loop forever`

### Binary Assertions > Subjective Scoring

Define quality as true/false checks, not ratings:
- Output is under 300 words → true/false
- No m-dashes used → true/false
- Contains exactly one CTA → true/false
- Opens with a hook, not a label → true/false

### Built-In Evals (Skills 2.0)

**Bad eval prompt:** "Run some tests on my skill"
**Good eval prompt:** "Run 5 tests optimized for: 1) always uses reference file, 2) uses curiosity hooks, 3) includes proof. Test on: writing landing page copy for X."

Evals produce HTML reports with per-run scoring, benchmark data, side-by-side outputs, and parallel execution via sub-agents.

### A/B Testing

Test whether a skill earns its context cost:
- Run prompt N times with skill → score against criteria
- Run prompt N times without skill → score against same criteria
- Compare scores AND token usage

### Iteration Discipline

Focus on **1-3 criteria** per eval cycle. First 1-3 runs feel AI-generated. By 10-30 runs, quality is production-grade. Each iteration bakes in knowledge from previous runs.

## Token Optimization

- **Hardcode static values** (API endpoints, IDs) instead of letting agent search each time
- **Delegate heavy searches to sub-agents** — keeps main skill context clean
- **Local markdown > API calls** — scrape docs once into reference.md

## Debugging Table

| Symptom | Fix |
|---------|-----|
| Wrong steps or order | Edit skill.md instructions |
| Missing tone/context | Add reference files |
| Same mistake repeating | Add explicit constraint |
| Struggles with tool/MCP | Create reference doc for it |
| Works but could be better | Brute force — run 10-30 times, nitpick |
| Skill doesn't trigger | Check YAML description — more specific keywords |
| Skill triggers too often | `disable_model_invocation: true` (slash-command only) |
