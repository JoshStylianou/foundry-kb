# KB Scaling Protocol

## Current Architecture (as of April 2, 2026)

- Two-tier: Core (17 entries in INDEX.md) + Reference (46 entries in domain DOMAIN_INDEXes)
- Session start loads: INDEX.md (~85 lines) + all DOMAIN_INDEXes (~100 lines) = ~185 lines total
- ai_and_agents DOMAIN_INDEX uses section headers for scanability
- Agents read full entries on-demand (1-3 per task)

## Scaling Thresholds

| Trigger | When | Action |
|---------|------|--------|
| Any domain exceeds 50 Reference entries | Split into sub-domains | Create 2-3 sub-domains with their own DOMAIN_INDEX. Parent domain becomes a routing index. |
| Core exceeds 25 entries | Add Core clusters | Group Core entries under section headers in INDEX.md (like ai_and_agents DOMAIN_INDEX already does for Reference). |
| Total index load exceeds 300 lines | Selective loading | Change session-start-protocol to load only INDEX.md + task-relevant domain indexes, not all. |
| Total entries exceed 150 | Consolidation sweep | Review all entries for: merge candidates (>80% overlap), archive candidates (unverified >90 days), demotion candidates (Core entries unreferenced 60+ days). |
| Index one-liners exceed 120 chars | Trim descriptions | One-liners in indexes must stay scannable. If they're getting long, the entry name should carry more weight. |

## Domain Split Protocol

When a domain splits:
1. Create sub-domain folders under the parent: `domains/ai_and_agents/agent_architecture/`, etc.
2. Each sub-domain gets its own DOMAIN_INDEX.md
3. Parent DOMAIN_INDEX becomes a routing table pointing to sub-domains
4. Full entry files move into their sub-domain folder
5. Update all `related:` links in affected entries
6. Update INDEX.md domain table with sub-domain counts

## Context Budget Math

| Component | Current Lines | At 150 entries | At 300 entries |
|-----------|--------------|----------------|----------------|
| INDEX.md Core table | ~25 | ~35 | ~45 (needs clusters) |
| All DOMAIN_INDEXes | ~100 | ~180 | ~350 (needs selective loading) |
| Total session start | ~185 | ~275 | ~455 (over threshold) |

At 1M context, 500 lines of index is ~1% of capacity — still trivial in absolute terms. The concern is not token cost but scanability: can an agent read 300+ one-liners and reliably pick the right 3? Testing suggests yes up to ~200, degradation above that.

## External Project Access

Every external project that references the KB should include a standard access block in its CLAUDE.md. See `references/kb-access-standard.md`.
