---
name: Entity Disambiguation Schema Drives AI Citations Over FAQ Schema
description: SameAs, knowsAbout, Organization schema produces 1.8x more AI citations than Article schema alone — FAQ/Review schema being devalued
type: insight
domain: growth_marketing
source: Digital Applied (April 2026), Schema.org v30.0 (March 19, 2026)
confidence: medium-high
date_added: 2026-04-08
date_verified: 2026-04-08
tags: [schema, structured-data, geo, ai-citations, json-ld]
related: [bing_chatgpt_citation_pipeline.md, ai_citation_freshness_decay.md]
---

## Core Principle

Entity disambiguation schema is now the highest-leverage structured data for AI citation. Google's March 2026 core update reduced rich result display for abused FAQ/Review/How-To schema on non-primary pages.

## Evidence

- Pages with full JSON-LD triple stack (Organization + Person + SameAs + knowsAbout) get 1.8x more AI citations than Article schema alone
- Schema.org v30.0 released March 19, 2026
- Google March 2026 core update specifically devalued FAQ/Review schema abuse

## Priority Schema for AI Citation

1. **Organization** — establishes entity identity
2. **Person** (for authors) — with knowsAbout, sameAs links to authoritative profiles
3. **SameAs** — cross-references to Wikipedia, LinkedIn, Crunchbase, official profiles
4. **Speakable** — marks quotable passages for voice/AI extraction
5. **Article** with full author attribution

## When to Apply

Update Styfinity's schema implementation playbook. Entity disambiguation should be the priority, not FAQ schema. The 1.8x multiplier is a strong ROI argument for structured data work in GEO engagements.

## Boundaries

Schema alone doesn't create authority — it surfaces existing authority to machines. A SameAs link to an empty LinkedIn profile adds nothing.
