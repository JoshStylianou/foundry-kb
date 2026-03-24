---
name: Team Roster Dynamic Loading with Hardcoded Fallback
description: Load team roster from API at startup, fall back to hardcoded config on failure, for internal vs external classification
type: pattern
domain: tools_and_software
source: First-party implementation — Slack EA project (production)
confidence: high
date_added: 2026-03-24
tags: [slack, team-roster, resilience, fallback, api, automation]
related: [slack_reaction_aware_signal_detection.md]
---

## The Problem

Many automated Slack workflows need to distinguish "internal team" from "external/client" users. This classification drives:
- Unanswered message detection (external message with no internal reply)
- Reaction acknowledgement (only internal reactions count)
- Name resolution in summaries (display name vs. user ID)
- Mention resolution (who was @mentioned)

Hardcoding the roster is brittle — people join and leave. But depending solely on the API is fragile — permissions change, rate limits hit, API outages happen.

## The Pattern: Try API, Fall Back to Config

### Architecture

1. **At startup**, call Slack's `users.list` API to get the full workspace roster
2. **Filter** to active, non-bot members who belong to the internal team (by domain, by user group, or by explicit list)
3. **If the API call fails** (permissions error, rate limit, timeout), fall back to a hardcoded roster in config:
   ```json
   {
     "fallback_team": [
       { "id": "U123ABC", "name": "Jane Smith", "email": "jane@company.com" },
       { "id": "U456DEF", "name": "John Doe", "email": "john@company.com" }
     ]
   }
   ```
4. **Store in mutable module-level state** with getter/setter functions:
   ```javascript
   let teamRoster = [];
   function setTeamRoster(roster) { teamRoster = roster; }
   function getTeamIds() { return teamRoster.map(m => m.id); }
   function getTeamNames() { return new Map(teamRoster.map(m => [m.id, m.name])); }
   ```

### Why Module-Level Mutable State

The roster is loaded once at startup and referenced throughout the application. Passing it as a parameter through every function call adds noise. Module-level state with explicit getters is the pragmatic choice for this pattern — the data is set once and read many times.

### Fallback Roster Maintenance

The fallback roster should be updated whenever team changes happen. It does not need to be perfectly current — it's a safety net, not the primary source. Monthly review is sufficient for most teams.

## Where Applied

- **Slack EA project:** `setTeamRoster()` / `getTeamIds()` / `getTeamNames()` in the main module, with fallback roster in config

## Pitfalls

1. **Stale fallback:** If the API has been failing silently for months and the fallback is outdated, new team members will be classified as "external." Log when falling back so you know it's happening.
2. **Bot users:** Filter out bot users from the roster — they are neither internal nor external. Slack's users.list includes bots by default.
3. **Multi-channel guests:** Slack guest accounts may be "internal" for some purposes but not others. Decide upfront whether guests count as internal.
4. **Large workspaces:** users.list is paginated. For workspaces with 1000+ members, handle pagination or you'll only get the first page.
