# Security Domain — Reference Library

**Purpose:** Core security patterns, threat models, and implementation guidance for everything built through The Foundry pipeline.

**When to load:** Any build that is public-facing, handles credentials, processes payments, stores PII, integrates third-party services, or exposes APIs.

---

## Entries

| Entry | Confidence | Pattern |
|-------|-----------|---------|
| [fail_closed_by_default](fail_closed_by_default.md) | high | Systems must deny access on error, not grant it. The most common security bug is an exception handler that lets the request through. |
| [trust_boundary_validation](trust_boundary_validation.md) | high | Validate and sanitize at every trust boundary crossing — user input, external APIs, webhooks, inter-service calls. Never trust data that crossed a boundary. |
| [secrets_lifecycle](secrets_lifecycle.md) | high | Secrets belong in environment variables or vaults, never in code. Static secrets rot. Every credential needs a rotation plan. |
| [least_privilege_principle](least_privilege_principle.md) | high | Every component, service account, and API key gets the minimum permissions required. Over-scoped credentials are the #1 cause of lateral movement after a breach. |
| [api_security_checklist](api_security_checklist.md) | high | Production API hardening: auth on every endpoint, rate limiting, input validation, no data leakage in errors, CORS/CSP headers, webhook signature verification. |
| [threat_modeling_for_builders](threat_modeling_for_builders.md) | medium-high | Lightweight STRIDE-based threat modeling adapted for The Foundry's build pipeline. Not a formal security audit — a practical checklist that catches 80% of issues. |
| [lethal_trifecta_agent_security](lethal_trifecta_agent_security.md) | high | Three-condition agent vulnerability: private data + untrusted content + outbound actions = exploitable. Remove any one leg to eliminate. |
