---
name: fail_closed_by_default
description: Systems must deny access on error states, not grant it. Covers error handling, auth failures, timeout behavior, and exception paths.
type: pattern
source: OWASP Secure Design Principles, CWE-280 (Improper Handling of Insufficient Permissions)
confidence: high
date_added: 2026-03-26
date_verified: 2026-03-26
domain: security
---

# Fail Closed by Default

## Principle

When a system encounters an error, timeout, or unexpected state, it must **deny access** — not grant it. "Fail open" is the most common security bug in production systems because developers design for the happy path and treat errors as edge cases.

## What This Means in Practice

**Auth checks that throw exceptions:**
```
// WRONG — fail open
try {
  const user = await verifyToken(token);
  return handleRequest(user);
} catch (err) {
  // Exception = no auth check = request proceeds
  return handleRequest(null);
}

// RIGHT — fail closed
try {
  const user = await verifyToken(token);
  return handleRequest(user);
} catch (err) {
  return Response(403, "Access denied");
}
```

**Timeout behavior:**
- If an auth service is unreachable, deny the request — do not skip auth.
- If a rate limiter is down, deny requests — do not allow unlimited access.
- If a permissions check times out, treat as "no permission."

**Default deny in access control:**
- Start with zero permissions, add explicitly.
- Never start with full permissions and remove.
- If a role/permission is not explicitly granted, it is denied.

## When to Apply

- Every error handler in auth/authz code paths
- Every timeout configuration for security-critical services
- Every access control system (RBAC, ABAC, API scopes)
- Every webhook validation — if signature check fails, reject the payload

## Anti-patterns to Reject

- `catch (err) { next() }` in auth middleware — silently passes through on failure
- `if (!user) { user = defaultUser }` — creating a fallback identity when auth fails
- Rate limiter that disables itself when Redis is down
- Feature flags that default to "enabled" for security controls
