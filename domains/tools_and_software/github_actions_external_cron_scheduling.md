# Replacing GitHub Actions Cron with External Cron Service

**Domain:** tools_and_software
**Created:** 2026-03-24
**Last verified:** 2026-03-24
**Confidence:** high
**Source:** First-party implementation (Slack EA project), corroborated by GitHub community documentation
**Tags:** github-actions, cron, scheduling, reliability, cron-job-org, workflow-dispatch

---

## The Problem

GitHub Actions `schedule:` cron triggers are unreliable for time-sensitive deliveries. Observed delays of 1-5+ hours are common and well-documented in GitHub community discussions. This is not a bug -- it is by design. GitHub makes no timing guarantees for cron-triggered workflows.

**If your workflow needs to run at a specific time (e.g., a morning brief at 07:00), GitHub Actions cron is not fit for purpose.**

---

## The Fix: External Cron + workflow_dispatch

Replace the scheduler, not the execution platform. Use cron-job.org (free tier) to trigger GitHub Actions `workflow_dispatch` endpoints on a precise schedule.

### Pattern

1. **Strip all `schedule:` triggers** from the GitHub Actions workflow file
2. **Keep only `workflow_dispatch`** with explicit input parameters
3. **Create external cron jobs** on cron-job.org that POST to the GitHub API dispatch endpoint
4. Result: second-accurate timing instead of hour-variable GitHub cron

### Workflow YAML Structure

```yaml
on:
  workflow_dispatch:
    inputs:
      brief_type:
        description: 'Type of brief to generate'
        required: true
        type: string
```

The `workflow_dispatch` input parameter passes the brief_type (or any parameter) directly, eliminating the need for a cron-to-type mapping step in the workflow.

---

## cron-job.org Configuration

### API Reference

- **Endpoint:** `PUT https://api.cron-job.org/jobs` (create/update)
- **Auth:** Bearer token from cron-job.org account
- **Rate limit:** 5 requests per minute on free tier
- **Free tier:** Sufficient for most use cases (supports multiple jobs)

### Schedule Format

Uses arrays for schedule fields:

| Field | Type | Wildcard | Example |
|-------|------|----------|---------|
| `hours` | int array | `[-1]` = every hour | `[7]` = 7am |
| `minutes` | int array | `[-1]` = every minute | `[0]` = on the hour |
| `wdays` | int array | `[-1]` = every day | `[1,2,3,4,5]` = weekdays |
| `mdays` | int array | `[-1]` = every day | `[1]` = 1st of month |
| `months` | int array | `[-1]` = every month | `[1,6]` = Jan and Jun |

### HTTP Dispatch Configuration

```json
{
  "job": {
    "url": "https://api.github.com/repos/{owner}/{repo}/actions/workflows/{workflow_id}/dispatches",
    "enabled": "true",
    "saveResponses": true,
    "schedule": {
      "timezone": "Europe/London",
      "hours": [7],
      "minutes": [0],
      "wdays": [1, 2, 3, 4, 5],
      "mdays": [-1],
      "months": [-1]
    },
    "requestMethod": 1,
    "extendedData": {
      "headers": "Accept: application/vnd.github+json\nAuthorization: Bearer ghp_YOUR_PAT\nX-GitHub-Api-Version: 2022-11-28\nUser-Agent: cron-job.org",
      "body": "{\"ref\":\"main\",\"inputs\":{\"brief_type\":\"your_type_here\"}}"
    }
  }
}
```

**Note:** `requestMethod: 1` = POST.

### GitHub PAT Requirements

- **Token type:** Classic (not fine-grained -- fine-grained tokens have different scope syntax)
- **Scopes needed:** `repo` + `workflow`
- **Expiration:** Can be set to "No expiration" on classic tokens
- Store the PAT in the cron-job.org job's `extendedData.headers` Authorization field

---

## When to Apply This Pattern

| Situation | Use GitHub Cron | Use External Cron |
|-----------|----------------|-------------------|
| Timing tolerance > 2 hours | Yes | Overkill |
| Time-sensitive delivery (briefs, alerts) | No | Yes |
| Needs to run at exact clock time | No | Yes |
| Simple nightly batch job | Yes | Unnecessary |
| User-facing scheduled output | No | Yes |

---

## Where Applied

- **Slack EA project:** `slack-brief.yml` workflow for MD and Leadership briefs (10 scheduled jobs total covering weekday, weekend, and Friday review schedules)

---

## Pitfalls

1. **cron-job.org timezone:** Set explicitly per job. Do not assume UTC -- use the timezone your users expect (e.g., `Europe/London` for UK delivery times).
2. **GitHub API rate limits:** Dispatches count toward your GitHub API rate limit (5,000/hour for authenticated requests). Not a concern for scheduled briefs, but relevant if you scale to hundreds of jobs.
3. **PAT rotation:** Classic tokens with no expiration are convenient but a security trade-off. If the repo is sensitive, use a shorter expiration and build a rotation process.
4. **Debugging:** Enable `saveResponses: true` on cron-job.org jobs to see GitHub's response codes. A 404 usually means wrong workflow ID or repo path. A 422 means malformed dispatch payload.
