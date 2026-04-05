# COO Layer — Learnings

## What Worked
1. **Reading all source files before writing anything** — every status value was verified against the real file. Zero placeholders.
2. **Context budget constraint** — forcing 500-line max and 100-line-per-file cap keeps the COO session useful after boot instead of context-starved.
3. **Relative paths in the registry** — makes the system portable and readable.
4. **State normalization for LinkedIn and YouTube** — the COO doesn't need to parse posts-history.md (69 lines of detailed post metadata) when a 20-line status.md gives the dashboard view.

## What the Next Version Should Do
1. **Auto-update "Last active" in departments.md** — currently manual. Could be set by the COO reading file modification dates.
2. **Add a "last briefing" timestamp** — so Josh knows when the COO last ran. Currently no persistent record.
3. **Consider per-department staleness thresholds** — LinkedIn is weekly, YouTube may go 2 weeks between meaningful updates. 7-day universal threshold may generate noise for YouTube.
4. **Newsletter state file** — if newsletter sending starts and grows beyond the simple sent-log, a Website/state/status.md may be warranted.
5. **Content graph automation** — once campaigns exceed ~8, manual maintenance becomes friction. A lightweight auto-scan (checking if blog slugs exist, if scripts exist) could assist.

## Integration Pattern
The COO layer follows the "coordinator reads, departments write" pattern. This is the same single-writer principle used in the LinkedIn and SEO departments individually. The pattern works because each CLAUDE.md defines its own context and quality rules — a parent session cannot replicate that context without duplicating it.
