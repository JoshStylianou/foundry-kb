# KB Entry Standard — The Foundry

## What the KB Is

A pattern library that makes Stark a genuinely exceptional advisor. Every entry is a **universal building pattern with real-world evidence** — knowledge that lets Stark recommend the right approach for a forex tool, a home shopping app, a marketing automation system, or a consulting framework with equal confidence.

**The test for every entry:** "Does this make Stark smarter at building things Josh hasn't asked for yet?"

The KB is NOT a news feed, tool changelog, summary library, bookmark collection, or tips-and-tricks list.

The KB IS: proven patterns with concrete evidence, universal across domains, immediately actionable, honest about where they break.

## Why Evidence Matters

Generic LLMs already know generic patterns. What makes Stark's advice worth more is cited proof: "Google proved this across 892 accounts with 23% better CPA at 91% reach." Evidence turns pattern-matching into genuine expertise. The format below enforces this.

---

## Entry Format

### Frontmatter

```yaml
---
name: [Pattern name — concrete, active voice, no tool/company names in the title]
description: [One sentence — specific enough that Stark can judge relevance from INDEX.md alone]
domain: [where primary evidence was observed — ai_and_agents | growth_marketing | forex_trading | business_operations | tools_and_software | meta_learning]
source: [primary source — author/publication, date]
confidence: high | medium
date_added: YYYY-MM-DD
date_verified: YYYY-MM-DD
tags: [both domain-specific AND universal terms for discoverability]
related: [filenames of related entries]
---
```

**Naming rule:** Name the pattern, not the source.
- Bad: "Google AI Max for Search Campaigns"
- Bad: "Meta Andromeda Update March 2026"
- Good: "Augmentation layers outperform full replacements on mature systems"
- Good: "Input diversity beats input precision when selection is AI-powered"

### Body

```markdown
## Pattern

[The universal principle in 1-3 sentences. Transferable across domains — if removing every product/company name makes it meaningless, it's not a pattern yet.

Concrete enough to ACT on. "Use layers" is too vague. "Add an optimization layer to existing workflows rather than replacing them — the layer gets 80-90% of a replacement's reach at significantly lower risk and cost" is actionable.]

## Evidence

[Real-world observations that PROVE the pattern. This section separates Stark from a generic LLM.

Required:
- Specific numbers: conversion rates, cost improvements, adoption metrics, scale of deployment
- Named implementations: companies, products, datasets — as evidence, not subject
- Source attribution: who published, when, based on what data

Multiple evidence points from different domains strengthen the pattern. Format as structured data (tables, numbered items) when possible.]

## Application Trigger

[When Stark should reach for this pattern. Conditional statements, domain-agnostic.

"Use this when..." format. Name 2-3 concrete examples across different domains.

Bad: "Use when optimizing Google Ads campaigns"
Good: "Use when adding AI capabilities to any existing system that already works — trading signals, project management, creative workflows. The more mature the base system, the stronger this pattern holds."]

## Boundaries

[When this pattern does NOT apply. Every pattern has limits.

Required:
- At least one condition where the opposite approach wins
- Scale or maturity thresholds where the pattern breaks
- Common misapplications to warn against

This section is what makes Stark's advice nuanced rather than dogmatic.]
```

### Reference Entries (Exception)

A small number of entries may be **living reference tables** — capability maps, pricing comparisons, tool inventories. These:
- Use `type: reference` in frontmatter
- Link to the pattern entry they serve
- Contain data that changes frequently and can't be embedded in a pattern entry
- Must be re-verified on schedule (typically monthly)

Reference entries must remain under 10% of the KB. The KB is patterns, not a database.

---

## Quality Gate

Every entry must pass ALL five tests before writing:

### 1. Pattern Test
State the pattern without naming a specific tool, product, or company. If the pattern collapses without "Google" or "Claude" or "Meta" — it's a feature description, not knowledge.

### 2. Evidence Test
The evidence includes at least one specific number, benchmark, or documented outcome from a real deployment. Patterns without quantified evidence are opinions.

### 3. Transfer Test
Name at least two different domains (marketing, trading, personal tools, consulting, infrastructure) where this pattern would inform a build decision. Single-domain knowledge isn't universal.

### 4. Boundary Test
Name at least one realistic situation where this pattern would be the WRONG approach. "This always works" is a red flag — it means you haven't stress-tested the pattern.

### 5. So-What Test
Stark reads this at 2am while advising on a completely unrelated project. Can he immediately use it? If only useful when the project involves [specific tool/domain], the entry is too narrow.

---

## Pattern Extraction Process

How to go from raw signal (news, transcript, research finding) to KB entry:

### Step 1: Strip the surface
Remove tool names, company names, domain specifics. What's left?
- "Google AI Max adds query matching to existing Search campaigns" becomes "An optimization layer was added to an existing system rather than replacing it"

### Step 2: Find the principle
What general rule explains WHY this worked?
- "The layer outperformed the full replacement because it preserved control and transparency while adding AI intelligence"
- Principle: augmentation layers outperform replacements on mature systems

### Step 3: Find the evidence
What specific, quantified results prove this?
- 892-account study, 23% better CPA, 91% of reach maintained

### Step 4: Find the transfer
Where else does this apply?
- AI trading signals on top of manual analysis
- AI recommendations in existing project management
- AI suggestions overlaid on creative brief workflows

### Step 5: Find the boundaries
When does this NOT work?
- Base system is fundamentally broken (replacement wins)
- Optimization layer can't access the base system's internals
- Users need a clean break from legacy workflows

**If any step produces nothing meaningful, the signal isn't KB-worthy.**

---

## What Doesn't Belong

| Raw Signal | Why Not KB | What To Do |
|------------|-----------|------------|
| "Tool X launched feature Y" | Feature description, not a pattern | Extract the pattern, or skip |
| "Company X raised $Y" | News, no evidence for a principle | Skip |
| "Here's how to configure tool X" | Operational doc | Keep as internal docs, not KB |
| "AI is transforming industry X" | Generic claim, no evidence | Skip |
| "Expert says X is the future" | Opinion without quantified evidence | WATCH at most |
| Video summary: "He talked about A, B, C" | Summary, not extraction | Extract patterns from the content |

---

## Confidence Rules

Follow the confidence lifecycle in the kb-curator agent:
- Autonomous research caps at `medium`
- Promotion to `high` requires: Josh confirmation, dual-source corroboration, or official docs verification
- Evidence quality determines confidence, not source prestige
- See kb-curator.md for full promotion/demotion protocol
