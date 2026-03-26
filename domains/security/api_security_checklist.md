---
name: api_security_checklist
description: Production API hardening checklist — auth, rate limiting, input validation, error handling, CORS, webhook verification. Apply to every API built through the pipeline.
type: pattern
source: OWASP API Security Top 10 (2023), production incident patterns
confidence: high
date_added: 2026-03-26
date_verified: 2026-03-26
domain: security
---

# API Security Checklist

## Purpose

Every API built through The Foundry pipeline must pass this checklist before it is considered production-ready. This is not a "nice to have" — it is the minimum bar.

## The Checklist

### Authentication & Authorization
- [ ] Every endpoint requires authentication unless explicitly designed to be public (and documented as such)
- [ ] Auth tokens are validated on every request — not cached and assumed valid
- [ ] Authorization checks happen at the resource level, not just the endpoint level (user A cannot access user B's data even if both are authenticated)
- [ ] Token expiry is enforced — expired tokens are rejected, not silently accepted
- [ ] Failed auth attempts return generic messages ("invalid credentials") — never reveal whether the username or password was wrong

### Input Validation
- [ ] All request parameters are validated: type, length, format, range
- [ ] Request body schema is validated against an explicit definition
- [ ] File uploads are validated: type, size, content (not just extension)
- [ ] Query parameters used in database queries are parameterized — never concatenated into query strings
- [ ] Path parameters are validated — no path traversal (`../`) possible

### Rate Limiting
- [ ] Rate limits are applied per-user or per-IP, not globally
- [ ] Rate limits cover authentication endpoints (to prevent brute force)
- [ ] Rate limit responses include `Retry-After` headers
- [ ] Rate limiter fails closed — if the rate limiting service is down, deny requests

### Error Handling
- [ ] Error responses never include stack traces, internal paths, or SQL queries
- [ ] Error responses use standard HTTP status codes consistently
- [ ] Unhandled exceptions return 500 with a generic message — not raw error details
- [ ] Errors are logged server-side with full detail — but the client only sees sanitized messages

### Headers & Transport
- [ ] HTTPS only — HTTP redirects to HTTPS, HSTS header set
- [ ] CORS is configured to allow only expected origins — not `*` in production
- [ ] Content-Security-Policy header restricts resource loading
- [ ] `X-Content-Type-Options: nosniff` prevents MIME sniffing
- [ ] Response headers do not leak server software versions

### Webhooks (if applicable)
- [ ] Incoming webhooks verify signatures (HMAC or asymmetric) before processing
- [ ] Webhook endpoints are rate limited
- [ ] Webhook payloads have a maximum size limit
- [ ] Failed signature verification returns 401 and logs the attempt

### Data Exposure
- [ ] API responses include only the fields the client needs — no full database rows
- [ ] Sensitive fields (passwords, tokens, internal IDs) are never included in responses
- [ ] Pagination is enforced — no endpoint returns unbounded result sets
- [ ] Logging does not capture request bodies containing credentials or PII

## When to Apply

Every API endpoint built through The Foundry. No exceptions for "internal" APIs — internal today is external tomorrow. No exceptions for "prototypes" — prototypes that work tend to become production.
