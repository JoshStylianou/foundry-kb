---
name: Claude Code Context Management
description: Principles for managing Claude Code's finite context window — progressive disclosure, skill sizing, compression techniques
type: insight
source: AI Learning Knowledge Base — YouTube transcripts
confidence: high
date_added: 2026-03-21
---

## Core Principle: Context Is Milk

Context window is finite and perishable. Every token loaded is a token unavailable for reasoning. Treat context like milk — use what you need, don't hoard it, and clear it before it spoils.

## Context Rot Threshold

Claude Code's default context window is 200k tokens. Effectiveness **drops drastically at ~100-120k tokens** (50-60% utilisation). This is "context rot" — the model's ability to reason coherently nosedives in the back half of the window. Implication: treat 50-60% as the red zone, not 90%. Reset before you hit it, not after.

## Status Line for Context Monitoring

Rather than repeatedly running `/context`, configure a persistent status line that always shows context % used, current model, and working directory. Either prompt Claude to build it or copy a config snippet. This removes the friction of manual context checks and makes window management habitual.

## Operational Rules

- **Use /clear between unrelated tasks.** Stale context from a previous task degrades performance on the current one.
- **Compact proactively.** Don't wait for the system to force compaction — trigger it when you know the current working set is done.
- **Skills share context with the conversation.** A skill that loads 5,000 tokens of reference material leaves 5,000 fewer tokens for reasoning. This is the critical constraint most people miss.

## skill.md Sizing

- **Under 200 lines.** The skill.md is a table of contents, not an encyclopedia.
- **Skill descriptions have a 15,000 character limit.** This is the trigger text Claude uses to decide whether to activate the skill — keep it precise and keyword-rich.

## Progressive Disclosure (Three Tiers)

Load context in layers, not all at once:

| Tier | What | When Loaded | Example |
|------|------|-------------|---------|
| 1 | YAML front matter | Always (on every conversation) | Name, description, trigger keywords |
| 2 | skill.md body | On skill activation | Process steps, decision logic, guardrails |
| 3 | references/, scripts/, assets/ | Only when a specific step needs them | API docs, templates, executable scripts |

This is the single highest-leverage pattern for context efficiency. Most people dump everything into Tier 2 and wonder why Claude gets confused on long tasks.

## Compression Techniques

- **Mermaid diagrams compress context efficiently.** A flowchart that would take 500 words of prose can be expressed in 100 tokens of Mermaid syntax, and Claude reads both equally well.
- **Tables over paragraphs.** Structured data in table format uses fewer tokens and is parsed more reliably than equivalent prose.
