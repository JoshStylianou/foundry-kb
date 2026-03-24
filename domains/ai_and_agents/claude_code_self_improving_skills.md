---
name: Claude Code Self-Improving Skills
description: Auto-research loops, binary assertions, Skills 2.0 evals with HTML reports, A/B testing, feedback cycle, wrap-up learnings
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcripts
confidence: high
date_added: 2026-03-21
date_updated: 2026-03-24
tags: [skills, evals, self-improving, qa, assertions]
related: [claude_code_skill_architecture.md]
---

## The Pattern: Karpathy's Auto-Research Loop Applied to Skills

`make a change → run test → check score → keep or revert → loop forever`

Two layers handle different aspects of improvement.

## Layer 1: Trigger Tuning (Activation Quality)

Anthropic's built-in skill creator handles this. It optimizes:
- Skill description wording
- Trigger keyword selection
- Activation precision (does Claude use the skill when it should, and not when it shouldn't?)

## Layer 2: Output Quality (Binary Assertion Loops)

Define quality as a set of true/false checks — no subjective scoring.

**Example assertions:**
- Output is under 300 words → true/false
- No m-dashes used → true/false
- Contains exactly one CTA → true/false
- Opens with a hook, not a label → true/false

### eval.json Structure

```json
{
  "tests": 5,
  "assertions_per_test": 5,
  "total_assertions": 25,
  "pass_threshold": "20/25 minimum"
}
```

## Skills 2.0: Built-In Evaluation & Testing

Anthropic's updated skill creator skill now includes proper evals. Not just "did it work" — you get actual grades against specific criteria.

### How to Use Evals Effectively

**Bad:** "Run some tests on my copywriting skill" → generic, useless results.

**Good:** "Run a new test optimized for making sure my copy follows the persuasive techniques listed in my persuasion toolkit reference file. Criteria: 1) always uses reference file, 2) uses curiosity and open loops, 3) uses proof or founder-led stories. Test on: writing landing page copy for X. Run 5 times."

### What You Get Back

- **HTML report** — clickable, browsable evaluation of all runs
- **Per-run scoring** against your specified criteria (pass/fail per criterion)
- **Benchmark data** — time per run, tokens per run
- **Side-by-side outputs** — flick between different runs
- **Parallel execution** — evals run multiple variations using sub-agents simultaneously

### A/B Testing: With vs Without Skill

Test whether the skill actually improves output or just costs tokens:
- Run same prompt N times with skill active
- Run same prompt N times without skill
- Compare scores against identical criteria
- Also compare token usage and time

This answers: "Is this skill earning its context cost, or should I strip/simplify it?"

### Iteration Discipline

Focus on **1-3 criteria** per eval cycle. Too many moving parts = no signal. Test → improve → retest → move to next criteria set.

## The Feedback Cycle

1. **Invoke** the skill
2. **Watch** the agent work (critical for first few runs)
3. **Give feedback** on what to improve
4. **Agent fixes** the skill.md
5. **Repeat**

First 1-3 runs feel AI-generated. By 10-30 runs, quality is production-grade. The skill compounds — each iteration bakes in knowledge from every previous run.

**Why watching matters:** You spot token waste (agent searching for the same thing every time), unnecessary steps, missing context. These optimizations can't be found by reading the output alone.

## Wrap-Up Skill: Session Learning Capture

At the end of each session, a wrap-up skill:
1. Reviews what was built or changed
2. Extracts learnings (what worked, what failed, edge cases discovered)
3. Writes findings to `learnings.md` within the relevant skill folder

**Critical maintenance: prune learnings weekly.** Without pruning, learnings.md grows until it becomes context bloat. Keep only learnings that changed behaviour.
