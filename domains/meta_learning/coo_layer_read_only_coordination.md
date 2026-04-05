---
name: COO Layer Read-Only Coordination Pattern
description: Cross-project coordination layers should read from child project state files but never write to them. Single-writer principle prevents merge conflicts and stale data.
type: pattern
domain: meta_learning
source: First-party implementation — Styfinity COO Layer architecture (April 2026)
confidence: medium-high
date_added: 2026-04-05
date_verified: 2026-04-05
tags: [coordination, state-management, multi-project, single-writer, architecture]
related: [watch_item_escalation_across_brief_cycles.md, shift_based_handoff_for_sustained_autonomous_work.md]
---

## Pattern

When building a coordination layer across multiple projects/repos, the coordinator reads from child state files but never writes to them. Each project has exactly one writer for its state (its own session/agent). The coordinator dispatches work by telling the operator which project session to open, not by directly modifying project files.

## Why

- Each project's CLAUDE.md defines session-specific context (voice rules, quality bars, skill triggers). A parent-level session writing to child state lacks that context.
- Git repos with multiple writers create merge conflicts and unclear ownership.
- State files with a single writer are always internally consistent. Multiple writers create race conditions even in manual workflows.

## Application

- Parent-level operating systems reading from child repos
- Cross-team dashboards reading from team state files
- Any system where a "manager" layer aggregates from "worker" layers

## Boundaries

- If the coordination layer needs to update state frequently (10+ times/day), the single-writer constraint creates too much friction. At that scale, use a shared database with proper concurrency.
- If projects are tightly coupled (changes in one require immediate updates in another), a shared state file may be more appropriate than separated state with coordination.
