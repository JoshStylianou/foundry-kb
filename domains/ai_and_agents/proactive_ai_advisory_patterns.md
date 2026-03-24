---
title: Proactive AI Advisory — Timing, Framing, and Competence Threat
domain: ai_and_agents
type: pattern
source: research_synthesis
confidence: high
date_added: 2026-03-22
date_verified: 2026-03-22
tags: proactive AI, advisory patterns, UX, competence threat, task boundaries, agent design
related: [claude_code_context_management.md]
---

## The Timing Rule

Proactive AI suggestions are welcomed at **task boundaries** (52% engagement rate post-commit) but actively dismissed mid-task (62% dismissal rate). The mechanism: at task boundaries, users have externalized their working memory and enter an evaluative mindset. Mid-task, suggestions compete for cognitive resources already allocated to implementation.

**Decision points** (when to advise): starting new work, finishing work, choosing between alternatives, reviewing what was built.
**Execution moments** (when NOT to advise): actively coding, debugging, following an already-decided plan.

## Competence Threat

Unsolicited AI help can trigger a **competence threat** — the user perceives the system as doubting their ability. This is strongest for:
- Skilled users who view competence as part of their identity
- Tasks the user has already started (implies their approach is wrong)
- Corrections framed as fixes rather than alternatives

**Mitigation:** Frame every suggestion as **adding an option**, never as **correcting an error**. Use additive language ("there's an approach worth considering") rather than corrective language ("you should do this differently").

## Three-Tier Proactive Model

| Tier | Risk Level | When | Example |
|------|-----------|------|---------|
| 1 — Always | Zero | Within scope of what was asked | Mention KB patterns when helping with implementation |
| 2 — At decision points | Low | Start/end of task, reviewing architecture | "Before we dive in — have you considered X?" |
| 3 — On invitation only | Higher | Cross-project observations, challenging past decisions | "I notice you're solving this differently in two projects" |

## Evidence

- CHI 2025: "Need Help? Designing Proactive AI Assistants for Programming"
- ArXiv 2601.10253: "Developer Interaction Patterns with Proactive AI: A Five-Day Field Study" (52% and 62% engagement figures)
- ArXiv 2509.09309: "Proactive AI Adoption can be Threatening" (competence threat mechanism)

## Why This Matters to The Foundry

Any Foundry agent designed to offer proactive advice (AI Consultant, future monitoring agents) must encode timing awareness. The default should be reactive, with proactive behavior activated only at task boundaries and decision points.

## Action Triggers

When building any agent that offers unsolicited suggestions: apply the three-tier model. When writing system prompts for advisory agents: encode "observe, note, wait for natural pause" rather than "interrupt with suggestions."
