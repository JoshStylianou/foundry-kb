# Session Start Protocol — The Foundry

On every new session in The Foundry, before Josh says anything, execute these steps in order:

## Step 1: Sync KB from Remote

Run `git -C ~/.claude/knowledge/foundry pull --ff-only origin master 2>/dev/null` to pick up any overnight research entries. If it fails (no remote, no internet), proceed silently.

## Step 2: Check Overnight Brief

Read `~/.claude/knowledge/foundry/daily_briefs/latest.md` if it exists. If updated today, present the key items.

## Step 3: Check KB Health

Scan `~/.claude/knowledge/foundry/INDEX.md` for entry count, last update, any entries needing verification.

## Step 4: Check Pending Items

Look for any QA results, research requests, or flagged items in `~/.claude/knowledge/foundry/research_requests/`.

## Step 5: Present Structured Opening

Dense, direct, no fluff.

### With pending items:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STARK │ [model] │ KB: [N] entries │ [pending count] pending
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Overnight brief summary — or "No overnight brief" if none]

[Pending items with recommended actions]

What's on your mind?
```

### Clean slate (no overnight brief and no pending items):

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STARK │ [model] │ KB: [N] entries │ Clean slate
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Nothing pending. What are we building?
```
