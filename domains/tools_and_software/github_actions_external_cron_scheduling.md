---
name: External cron triggers replace unreliable built-in schedulers
description: Replace GitHub Actions cron with external cron service (cron-job.org) + workflow_dispatch for second-accurate timing. Observed 1-5+ hour delays with built-in cron.
domain: tools_and_software
source: First-party implementation (Slack EA project), GitHub community documentation
confidence: high
date_added: 2026-03-24
date_verified: 2026-03-24
tags: [github-actions, cron, scheduling, reliability, cron-job-org, workflow-dispatch, automation]
related: []
---

## Pattern

When a CI/CD platform provides a built-in cron scheduler with no timing guarantees, replace the scheduler — not the execution platform. Use an external cron service to trigger the platform's dispatch API on a precise schedule.

This preserves all the benefits of the execution platform (environment, secrets, runners, integrations) while eliminating the timing unreliability.

## Evidence

- **GitHub Actions `schedule:` cron:** Observed delays of 1-5+ hours. This is by design — GitHub makes no timing guarantees for cron-triggered workflows. Well-documented in GitHub community discussions.
- **External cron (cron-job.org) + `workflow_dispatch`:** Second-accurate timing. Free tier sufficient for most use cases.
- **First-party deployment:** Slack EA project — 10 scheduled jobs covering weekday, weekend, and Friday review schedules. All delivering within seconds of target time.

### Implementation Pattern

1. Strip all `schedule:` triggers from the workflow file
2. Keep only `workflow_dispatch` with explicit input parameters
3. Create external cron jobs that POST to the GitHub API dispatch endpoint
4. Result: second-accurate timing instead of hour-variable GitHub cron

### cron-job.org Configuration

- **Endpoint:** `PUT https://api.cron-job.org/jobs` (create/update)
- **Auth:** Bearer token from cron-job.org account
- **Dispatch target:** `https://api.github.com/repos/{owner}/{repo}/actions/workflows/{workflow_id}/dispatches`
- **GitHub PAT requirements:** Classic token (not fine-grained), scopes: `repo` + `workflow`

## Application Trigger

Use this when any scheduled system needs precise timing and the built-in scheduler is unreliable:
- CI/CD pipelines that must run at specific times (morning briefs, scheduled reports, time-sensitive deployments)
- Any automation platform where the scheduler and the executor can be decoupled
- Cron-based monitoring or alerting where delay defeats the purpose

## Boundaries

- **Overkill for loose timing:** If delivery within a 2+ hour window is acceptable, built-in cron is simpler and sufficient
- **External dependency:** Adds cron-job.org as a dependency. If it goes down, your schedules stop. Acceptable for non-critical workflows, risky for mission-critical ones without a fallback
- **PAT security:** Classic tokens with no expiration in a third-party service are a security trade-off. Use shorter expiration and build rotation process for sensitive repos
- **GitHub API rate limits:** Dispatches count toward the 5,000/hour authenticated request limit. Not a concern for scheduled briefs, relevant at hundreds of jobs
