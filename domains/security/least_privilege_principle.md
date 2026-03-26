---
name: least_privilege_principle
description: Every component, service account, and API key gets minimum permissions required. Over-scoped credentials are the top cause of lateral movement after a breach.
type: pattern
source: NIST SP 800-53 (AC-6), principle of least privilege
confidence: high
date_added: 2026-03-26
date_verified: 2026-03-26
domain: security
---

# Least Privilege Principle

## Principle

Every component, user, service account, and API key operates with the **minimum permissions required** to perform its function. Nothing more. Over-scoped access doesn't cause breaches — it determines how bad a breach gets.

## How to Apply

### API Keys & Tokens
- If a service only reads data, it gets a read-only key.
- If a service only accesses one table, it gets scoped to that table.
- If a GitHub Action only needs to read repo contents, it does not get `repo` scope (which includes write, delete, admin).
- Review scopes at creation time. Default scopes are almost always too broad.

### Service Accounts
- One service account per service. Never a shared "admin" account used by multiple services.
- Service accounts do not get interactive login capabilities.
- Service accounts are audited: if a service is decommissioned, its account is revoked.

### Database Access
- Application accounts get access to the tables they need, not the entire database.
- Supabase Row Level Security (RLS) enforces access at the data layer, not just the application layer.
- Migration accounts and application accounts are separate — migrations need schema change permissions, the running app does not.

### File System & Infrastructure
- Containers run as non-root unless there is a specific, documented reason.
- File permissions follow principle: owner can read/write, group can read, others have no access.
- Cloud IAM roles are scoped to the specific resources and actions needed.

### Human Access
- Admin access is for admin tasks. Day-to-day work uses standard permissions.
- Access is granted for the duration needed, then revoked (time-bounded access).

## Blast Radius Thinking

When granting permissions, ask: **"If this credential is leaked, what can an attacker do with it?"**

| Scope | Blast radius if leaked |
|-------|----------------------|
| Read-only, single resource | Low — attacker sees one thing |
| Read-write, single resource | Medium — attacker can modify one thing |
| Read-write, multiple resources | High — attacker can modify many things |
| Admin, full account | Critical — attacker owns everything |

Design for the breach. Assume every credential will eventually be exposed. The question is: how much damage can it do when it is?

## Anti-patterns to Reject

- "Just give it admin access, it's easier" — easy for the attacker too
- A single API key shared across multiple services
- GitHub PATs with `repo` scope when only `read:packages` is needed
- Supabase `service_role` key used in client-side code
- IAM policies with `"Action": "*"` or `"Resource": "*"`
