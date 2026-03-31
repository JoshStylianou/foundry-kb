---
name: Dual-Loop System Prompt Improvement
description: Local loop (plan→build→learn→update project claude.md) + global loop (/insights→manual review→update global claude.md) — infinity-sign workflow for continuous improvement
type: insight
domain: ai_and_agents
source: Nick Saraev — "Definitive Claude Code Course for Advanced Users" (YouTube, ~2026)
confidence: medium-high
date_added: 2026-03-29
date_verified: 2026-03-29
tags: [claude-md, improvement-loops, insights, workflow, system-prompts]
related: [claude_code_self_improving_skills.md, claude_md_four_pillars_design.md]
---

## The Pattern: Two Nested Improvement Cycles

System prompt quality improves through two loops operating at different frequencies — like an infinity sign (∞).

### Local Loop (High Frequency — Every Feature)

```
Plan feature → Build/instantiate → Compile learnings → Update project claude.md → Repeat
```

1. **Plan** the feature (or task — "feature" is loose; includes any substantive work)
2. **Build** it. Along the way, Claude fails and succeeds in various ways.
3. **Ask Claude:** "How could you have arrived at these conclusions faster and for fewer tokens?" This surfaces concrete optimizations (e.g., "one write call instead of 20 sequential edits").
4. **Update the project claude.md** with the distilled learnings.

Each cycle through the local loop shaves ~10% off the next iteration's cost/time. The first few loops yield the biggest gains.

**Meta-prompt trick:** Include in claude.md: "When you make a mistake, update this file with what not to try next time." This automates step 3-4 without user intervention.

### Global Loop (Low Frequency — After Dozens of Local Loops)

```
Accumulate local learnings → Run /insights → Manual review → Update global claude.md → Return to local loop
```

1. After many local cycles across one or more projects, patterns emerge.
2. Run `/insights` — this scans all conversation history via sub-agents and surfaces cross-session patterns (what Claude consistently struggles with, what consistently works).
3. **Manually review** the insights output. This step is non-negotiable (see: probability decay below).
4. Distill into high-information-density bullet points for the global claude.md.

### Why Manual Review Is Required at the Global Level

Each Claude step is independently ~90% accurate. But accuracy compounds multiplicatively:
- 1 step: 90%
- 2 steps: 81%
- 3 steps: 73%
- 4 steps: 66%

The global claude.md affects *every future project*. If there's one place to spend human review time, it's this step. A bad local claude.md wastes tokens on one project. A bad global claude.md degrades everything.

### The /insights Integration

`/insights` runs sub-agents across all Claude conversation history and produces:
- Session count and message volume analyzed
- Cross-project patterns in Claude's behavior
- "Existing features to try" — concrete optimizations ready to paste into claude.md
- Suggested new skills based on repeated user requests

**Cadence:** Run /insights after every ~50-100 local loop iterations, or whenever you notice Claude making the same class of mistake across projects.

## Application Trigger

- Starting a new project: begin the local loop from session one
- Noticing cross-project patterns: trigger the global loop
- Periodic maintenance: run /insights monthly regardless

## Boundaries

- Don't run the global loop too frequently. You need enough local loop data for patterns to emerge.
- /insights output should be curated, not copy-pasted wholesale. High information density matters.
- The Karpathy auto-research loop (see: claude_code_self_improving_skills.md) is a related but distinct pattern — it applies to *skill* improvement via binary assertions. This dual-loop applies to *system prompt* improvement via experience accumulation.
