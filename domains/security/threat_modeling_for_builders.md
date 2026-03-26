---
name: threat_modeling_for_builders
description: Lightweight STRIDE-based threat modeling adapted for The Foundry pipeline. Practical checklist that catches 80% of security issues without formal security audit overhead.
type: pattern
source: Adam Shostack "Threat Modeling" methodology, Microsoft STRIDE, adapted for Foundry context
confidence: medium-high
date_added: 2026-03-26
date_verified: 2026-03-26
domain: security
---

# Threat Modeling for Builders

## Purpose

This is not a formal security audit. It is a lightweight, practical threat model that The Foundry's Architect and Builder teams use to catch the most common and damaging security issues before they are built into the system.

The goal: spend 15 minutes asking the right questions to prevent 80% of security incidents.

## STRIDE — Simplified

STRIDE is a threat classification framework. For each component in the architecture, ask whether it is vulnerable to each threat type:

| Threat | Question to Ask | Example |
|--------|----------------|---------|
| **S**poofing | Can someone pretend to be someone/something they're not? | Forged webhook payloads, stolen auth tokens, impersonated service accounts |
| **T**ampering | Can someone modify data they shouldn't? | Man-in-the-middle on HTTP, SQL injection to alter records, modifying request payloads |
| **R**epudiation | Can someone deny they did something, and we can't prove they did? | No audit logs, unsigned transactions, missing request logging |
| **I**nformation Disclosure | Can someone see data they shouldn't? | Verbose error messages, API over-fetching, logs containing PII, exposed .env files |
| **D**enial of Service | Can someone make this unavailable? | No rate limiting, unbounded queries, resource exhaustion, missing pagination |
| **E**levation of Privilege | Can someone do something they're not authorized to do? | Broken access control, IDOR (accessing other users' resources by changing an ID), missing role checks |

## How to Use in The Foundry Pipeline

### At Architecture (Chief of Architect)

For each component in the spec:
1. Draw the data flow: what data enters, from where, where it goes, what trust boundary it crosses
2. Run STRIDE against each trust boundary crossing
3. For each identified threat, document: the threat, the likelihood (low/medium/high), the impact (low/medium/high), and the mitigation
4. Include mitigations in the component spec — the Builder implements them

### At Build Review (Chief of Builder)

For each completed component:
1. Verify that every mitigation from the architecture's threat model is implemented
2. Run the API Security Checklist if the component exposes an API
3. Check that error paths fail closed
4. Verify secrets are not in code

### Quick Threat Assessment Matrix

For fast decisions on where to focus security effort:

| | Low Impact | High Impact |
|---|-----------|------------|
| **Low Likelihood** | Accept the risk, document it | Mitigate — high impact justifies effort even at low probability |
| **High Likelihood** | Mitigate — it will happen | **Critical** — mitigate immediately, this is a showstopper |

## Common Threats in Foundry Builds

Based on the types of systems The Foundry builds (AI agents, automation workflows, API integrations, Slack bots):

| System Type | Top Threats |
|------------|------------|
| **Slack bots** | Token theft (S), message tampering (T), missing audit logs (R), leaking channel data (I) |
| **n8n workflows** | Credential exposure in workflow JSON (I), webhook spoofing (S), unbounded execution (D) |
| **API integrations** | Token leakage in logs (I), missing auth on endpoints (E), rate limiting bypass (D) |
| **AI agent systems** | Prompt injection (T), over-scoped tool access (E), sensitive data in context windows (I) |
| **Supabase backends** | Missing RLS policies (E), exposed service_role key (I/E), SQL injection in custom queries (T) |

## Output

The threat model for a build should be a simple table, not a document:

```
| Component | Threat | Type | Likelihood | Impact | Mitigation |
|-----------|--------|------|-----------|--------|------------|
| /api/users | IDOR — user A accesses user B data | E | High | High | Row-level access check on every query |
| Webhook handler | Forged payload | S | Medium | High | HMAC signature verification |
| Error responses | Stack trace leakage | I | High | Medium | Generic error messages, server-side logging only |
```

This table goes in the Architecture Spec's Security Design section and becomes the Builder's implementation checklist.
