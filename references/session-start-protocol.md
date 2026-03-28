# Session Start Protocol — The Foundry

On every new session in The Foundry, execute these steps before Josh speaks.

## Step 1: Sync KB from Remote

Run `git -C ~/.claude/knowledge/foundry pull --ff-only origin master 2>/dev/null` to pick up overnight changes. If it fails, proceed silently.

## Step 2: Load Context (Silent)

Read `~/.claude/knowledge/foundry/INDEX.md` for Core patterns and KB health. Read `~/.claude/memory/MEMORY.md` if not already loaded. Check `~/.claude/knowledge/foundry/research_requests/` for pending items.

**Load all domain indexes for full KB visibility:**
Read every `~/.claude/knowledge/foundry/domains/*/DOMAIN_INDEX.md`. This gives you awareness of every Reference entry's title and one-liner (~89 lines total). You do NOT need to read full entries — just the indexes. When a task is relevant to a specific entry, read the full entry on-demand.

This ensures no KB entry is invisible regardless of how large the KB grows. The cost is trivial (~9KB) against a 1M context window.

Run a quick integrity check (silently — only surface problems):
- Does INDEX.md Core + Reference total match actual files?
- Are all file paths in CLAUDE.md still valid?
- Do domain index entry counts match actual .md files in each domain folder?

If any check fails, include it in the opening as a health warning. If all pass, say nothing.

## Step 3: Present Opening

Dense, direct, no fluff.

### With pending items:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STARK │ [model] │ KB: [N] entries ([C] Core) │ [status]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Any health warnings or pending research requests]

What are we building?
```

### Clean slate:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STARK │ [model] │ KB: [N] entries ([C] Core) │ Clean slate
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

What are we building?
```

## Daily Brief — Automatic on Session Start

The daily brief lives in #foundry-briefs. **Pull it automatically at session start.**

After the integrity check (Step 2), before presenting the opening:
1. Fetch Slack MCP schema via ToolSearch
2. Read latest messages from #foundry-briefs (channel ID: C0ANAU3RR1R)
3. Deduplicate KB signals against INDEX.md and domain indexes — silently drop anything already covered
4. For each new signal, include: **recommendation** (approve / reject / needs research), **proposed tier** (Core or Reference with reasoning), and **proposed confidence** (with justification based on evidence quality)
5. Present new signals in the opening with recommendations, or note "No new signals" if everything has been processed
6. Lead with the recommendation so Josh can approve or override quickly

## Rolling KB Freshness Check — Built Into the Brief

The daily brief also handles KB maintenance. No separate audit triggers needed.

**After processing new signals (step 5 above), before presenting the opening:**

1. Read all KB entry frontmatter and find the 2-3 entries with the oldest `last_verified` (or `date_verified`) dates
2. For each, run a quick web search to check whether the core claim still holds
3. Classify each as: **Still valid** (update verified date silently) | **May be outdated** (flag to Josh with evidence) | **Unable to verify** (note it, move on)
4. Include any flagged entries in the brief under a `KB FRESHNESS` section — only if something needs attention. If all checked entries are still valid, say nothing.

**Cadence math:** 2-3 entries/day × 30 days = 60-90 checks/month. At 59 entries, the entire KB is verified monthly with zero manual effort. As the KB grows to 200 entries, this still covers everything within ~3 months — well within the 6-month window for architecture patterns.

**Critical rule:** Rolling checks can update `last_verified` dates silently when confirmed still valid. They can flag entries for review. They CANNOT modify entry content, change confidence levels, or archive entries without Josh's approval.

## KB Entry Approval Protocol

**Critical rule: Never auto-write KB entries from the daily brief.**

When Josh approves a KB signal:
1. Assess tier: does it pass the Core test ("changes decisions across 2+ businesses")? If yes → Core. If no → Reference.
2. Assign honest confidence based on evidence quality (not default to high)
3. Write the entry, update the appropriate index (INDEX.md for Core, DOMAIN_INDEX.md for Reference)
4. Push to git
5. Confirm: "[entry name] written to KB at [confidence], [tier]."

When Josh says "needs more research":
1. Add to `research_requests/consultant_flags.md`

When Josh rejects:
1. Discard — no entry, no flag
