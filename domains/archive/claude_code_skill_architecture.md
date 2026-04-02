---
name: Claude Code Skill Architecture
description: Skill types, six-step build framework, file structure, activation, global vs project, debugging, advanced front matter
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcripts
confidence: medium-high
date_added: 2026-03-21
date_updated: 2026-03-24
date_verified: 2026-03-24
tags: [skills, claude-code, architecture, front-matter, evals]
related: [claude_code_self_improving_skills.md, claude_code_advanced_workflows.md]
---

## What Skills Are

Skills = reusable instructions. Write once, save as a skill, trigger anytime. They're SOPs for AI agents — same as training a human employee by giving them a process doc. Equivalent to the "W" in the WAT framework.

Skills aren't just text generators — they can run scripts, call APIs, spawn sub-agents, and be invoked by other agents. The more you run a skill, the better it gets through the feedback cycle.

## Two Types of Skills

| Type | Definition | Durability | Example |
|------|-----------|------------|---------|
| **Capability uplift** | Prompts that teach Claude to do something better | Fades as models improve | "Write concisely", "Use structured output" |
| **Encoded preference** | Sequential workflows specific to your business | Stays durable — model can never guess your process | "Publish to LinkedIn with our tone, formatting, and CTA pattern" |

**Implication:** Invest build time in encoded preference skills. Capability uplift skills are temporary scaffolding.

## Six-Step Skill Building Framework

1. **Name & trigger** — what it's called + natural language that fires it
2. **Goal** — one sentence: what will this skill accomplish? What's the output?
3. **Step-by-step process** — if you did this manually, what do you do, in what order, what decisions do you make?
4. **Reference files** — what context is needed? Brand voice, images, project state, style guides, API docs
5. **Rules/guardrails** — what could go wrong? Build in constraints
6. **Self-improvement loop** — test, iterate, watch the agent work, give feedback

## Skill File Structure

```
.claude/skills/skill-name/
├── skill.md          # Process/SOP (under 500 lines per official docs)
├── references/       # Knowledge loaded on demand
├── scripts/          # Executable code (Python, bash, etc.)
└── assets/           # Templates, examples, logos, sample outputs
```

**Reference file placement:** Two valid approaches:
- **Self-contained** — references/ and scripts/ nested under the skill folder
- **External** — files stored elsewhere in the project, pointed to by path in skill.md

Either works. The only rule: paths in skill.md must point to the right location. Claude reads the skill.md and follows the paths.

## Global vs Project Skills

| Location | Scope | When to Use |
|----------|-------|-------------|
| `.claude/skills/` (in project) | This project only | Project-specific workflows |
| `~/.claude/skills/` (home directory) | Every project, globally | Personal workflows, company context, front-end design |

## Progressive Context Loading (Three Tiers)

| Tier | What | Token Cost | When |
|------|------|------------|------|
| 1 | YAML front matter (name + description) | ~100 tokens | Every request — Claude scans all skills |
| 2 | Full skill.md body | 1,000–2,000 tokens | Only when skill is selected as relevant |
| 3 | References, scripts, assets | Variable | Only when a specific step needs them |

This is why skill descriptions must be precise — Tier 1 is the filter. Bad description = skill never gets past Tier 1.

## Skill Activation Rate

- **~20% activation rate** with generic/vague descriptions
- **~84% activation rate** with optimized descriptions containing specific trigger keywords

Include the exact phrases a user would naturally say. "Write a LinkedIn post" beats "social media content creation assistant."

## claude.md Sizing

- **20-30 lines max.** claude.md is a routing layer, not a knowledge store.
- **Point, don't dump.** claude.md should point to skills and reference files, not contain their content.
- **Reference files: 200-300 lines each.** If a reference file exceeds this, split it.

## Token Optimization in Skills

- **Hardcode static values** (e.g., ClickUp list IDs, API endpoints) instead of letting the agent search for them every invocation
- **Delegate heavy searches to sub-agents** — "delegate to the ClickUp searcher agent" keeps the main skill's context clean
- **Local markdown > API calls** — scrape docs once into a reference.md, read locally instead of web-searching every time

## Debugging Table

| Symptom | Fix |
|---------|-----|
| Wrong steps or wrong order | Edit skill.md instructions |
| Missing tone/style/context | Add reference files, ensure skill.md points to them |
| Same mistake repeating | Add an explicit rule/constraint |
| Struggles with a tool/MCP, keeps searching | Create a reference doc for it |
| Works but could be better | Brute force — run 10-30 times, nitpick each run |
| Skill doesn't trigger | Check YAML description — make it more specific |
| Skill triggers too often | Disable model invocation (slash-command only) |

## Advanced Front Matter Options

Beyond `name` and `description` (required), skills support:
- `allowed_tools` — restrict which tools the skill can use
- `argument_hint` — hint text shown when user types the slash command
- `model` — force a specific model for this skill
- `context` — additional context files to load
- `hooks` — pre/post execution hooks
- `agent` — run in a specific agent identity
- `disable_model_invocation: true` — only trigger via slash command, never via natural language
