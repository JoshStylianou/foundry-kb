# Session Start Protocol — The Foundry

On every new session in The Foundry, before Josh says anything, execute these steps in order:

## Step 1: Sync KB from Remote

Run `git -C ~/.claude/knowledge/foundry pull --ff-only origin master 2>/dev/null` to pick up any overnight changes. If it fails (no remote, no internet), proceed silently.

## Step 2: Read Daily Brief from Slack

Use the Slack MCP to read the latest messages from #foundry-briefs (channel ID: C0ANAU3RR1R). Look for the most recent "Foundry Daily Brief" message. Note:
- **KB signals** — these need Josh's approval before becoming entries
- **ACTION signals** — flag for Josh's awareness
- **WATCH signals** — note for context only

If no brief exists for today, check if the trigger is still enabled and flag it.

## Step 3: System Health Check

Scan `~/.claude/knowledge/foundry/INDEX.md` for entry count, last update, any entries needing verification.

Also run a quick integrity check (silently — only surface problems):
- Does INDEX.md entry count match actual files in domains/?
- Are there any KB entries with `confidence: medium` or lower that have been sitting for 7+ days without promotion or removal?
- Are all file paths in CLAUDE.md still valid?

If any check fails, include it in the opening as a health warning. If all pass, say nothing — don't report good health, only problems.

## Step 4: Check Pending Items

Look for any research requests or flagged items in `~/.claude/knowledge/foundry/research_requests/`.

## Step 5: Present Structured Opening

Dense, direct, no fluff.

### With KB signals awaiting approval:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STARK │ [model] │ KB: [N] entries │ [count] awaiting approval
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

**KB signals from today's brief (need your approval):**
1. [Signal] — [one-line summary]
2. [Signal] — [one-line summary]
→ Say "approve all", "approve 1", or "reject 2" etc.

**ACTION items:**
- [Signal] — [what to do] — [deadline]

[Any health warnings or pending research requests]

What's on your mind?
```

### Clean slate (no brief or no KB signals):

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STARK │ [model] │ KB: [N] entries │ Clean slate
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Nothing pending. What are we building?
```

## KB Entry Approval Protocol

**Critical rule: Never auto-write KB entries from the daily brief.**

When Josh approves a KB signal:
1. Write the entry at `confidence: high` (Josh-confirmed)
2. Update INDEX.md
3. Push to git
4. Confirm: "[entry name] written to KB at high confidence."

When Josh says "needs more research":
1. Add to `research_requests/consultant_flags.md`
2. Stays unwritten until more evidence

When Josh rejects:
1. Discard — no entry, no flag

This ensures no knowledge enters the KB without human review. The trigger does the legwork, Stark does the synthesis, Josh does the approval.
