---
name: trust_boundary_validation
description: Validate and sanitize data at every trust boundary crossing — user input, external APIs, webhooks, inter-service calls. Never trust data from outside.
type: pattern
source: OWASP Input Validation Cheat Sheet, Microsoft STRIDE threat model
confidence: high
date_added: 2026-03-26
date_verified: 2026-03-26
domain: security
---

# Trust Boundary Validation

## Principle

A trust boundary is any point where data moves between components with different trust levels. Data crossing a trust boundary is **untrusted by default** and must be validated before use — regardless of where it comes from.

## Common Trust Boundaries

| Boundary | Example | What to validate |
|----------|---------|-----------------|
| **User → Server** | Form submissions, API requests | Type, length, format, allowed values, encoding |
| **External API → Your system** | Third-party API responses, webhook payloads | Schema conformance, unexpected fields, malicious content |
| **Database → Application** | Query results | Data integrity (especially if DB is shared with other services) |
| **Service → Service** | Internal API calls in microservices | Auth tokens, request signatures, payload schema |
| **File system → Application** | Config files, uploaded files | File type verification, path traversal prevention, size limits |
| **Environment → Application** | Env vars, CLI args | Type validation, required value checks |

## Implementation Rules

1. **Validate at the boundary, not deep in business logic.** Validation belongs in the handler/controller/middleware — not buried three function calls deep where it might be bypassed.

2. **Allowlist over denylist.** Define what IS valid (allowed characters, expected formats, permitted values) rather than trying to block what isn't. Denylists always miss something.

3. **Validate type, length, format, and range.** A field being "present" is not validation. Check that it is the right type, within expected length, matches the expected format, and falls within a valid range.

4. **Sanitize output, not just input.** Even validated data must be properly encoded/escaped when rendered in HTML, SQL, shell commands, or logs. Validation prevents bad data from entering; output encoding prevents it from being interpreted as code.

5. **Never trust client-side validation alone.** Client-side validation is UX, not security. Every check must be repeated server-side.

## Webhook-Specific Rules

- Always verify webhook signatures (HMAC, asymmetric signatures) before processing payloads.
- Reject webhooks with missing or invalid signatures — do not process "just in case."
- Validate that the webhook source IP is from the expected provider (where providers publish IP ranges).
- Set a maximum payload size to prevent denial of service.

## Anti-patterns to Reject

- Trusting `req.body` without schema validation because "our frontend sends it correctly"
- Passing external API responses directly to business logic without checking the schema
- Using user-provided file paths without sanitizing for `../` traversal
- Logging raw user input without sanitization (log injection)
