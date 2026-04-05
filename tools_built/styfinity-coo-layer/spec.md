# Styfinity COO Layer

**Built:** 2026-04-05
**Type:** Local markdown coordination system (no code, no APIs)

## What It Is
A 5-file coordination layer at `C:/Users/joshs/Styfinity/` that gives Claude Code sessions a COO persona with cross-department visibility. On session start, it reads department state files and generates a morning briefing.

## Architecture
- `CLAUDE.md` — COO persona with boot sequence and briefing format
- `departments.md` — Registry of 4 departments (SEO, Website, LinkedIn, YouTube) with state file paths
- `content-graph.md` — Cross-department content tracker for 4 campaigns
- `Linkedin/state/status.md` — Normalized LinkedIn state summary
- `Youtube/state/status.md` — Normalized YouTube state summary

## Key Design Decisions
- COO reads department state, never writes to it (single-writer principle)
- Content graph is manual, not auto-generated (avoids brittle inference)
- Morning briefing is generated live, not persisted (always current)
- 500-line context budget on boot (100-line cap per state file)
- 7-day universal staleness threshold
- COO dispatches work to department sessions, doesn't execute it
