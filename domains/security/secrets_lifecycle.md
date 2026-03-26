---
name: secrets_lifecycle
description: Secrets belong in environment variables or vaults, never in code. Every credential needs a rotation plan. Covers storage, access, rotation, and revocation.
type: pattern
source: OWASP Secrets Management Cheat Sheet, 12-Factor App methodology
confidence: high
date_added: 2026-03-26
domain: security
---

# Secrets Lifecycle

## Principle

A secret (API key, token, password, connection string, private key) is a liability. Every secret that exists is a potential breach vector. The goal is: fewest secrets possible, shortest lifetime possible, narrowest access possible.

## Rules

### Storage
- **Never in code.** Not in source files, not in config files committed to git, not in comments, not in variable names that hint at the value.
- **Environment variables** for simple deployments. Loaded at runtime, not baked into images.
- **Secrets vaults** (GitHub Secrets, Supabase Vault, AWS Secrets Manager, etc.) for production systems.
- **`.env` files** for local development only — always in `.gitignore`. Never committed.
- **Never in logs.** Mask or redact secrets in any logging output. Check that error messages don't include connection strings or tokens.

### Access
- **Least privilege.** Each secret grants the minimum scope needed. A read-only operation does not need a read-write token.
- **Separate secrets per environment.** Dev, staging, and production each get their own credentials. Never share secrets across environments.
- **Separate secrets per service.** If two services need database access, they get separate credentials — not a shared one. This limits blast radius.

### Rotation
- **Every secret needs a rotation plan.** "It doesn't expire" is not a plan — it's a future incident.
- **Prefer short-lived tokens** (OAuth access tokens, JWTs with expiry) over long-lived API keys.
- **Classic PATs and static API keys** are acceptable for prototypes but must be flagged for rotation before production.
- **When rotating:** create the new secret, deploy it, verify it works, then revoke the old one. Never revoke first.

### Revocation
- **When a secret is compromised:** revoke immediately, rotate, audit access logs.
- **When a team member leaves or a service is decommissioned:** revoke all associated secrets.
- **Credential shared in chat, email, or logs:** treat as compromised. Rotate immediately.

## Foundry-Specific Guidance

- GitHub Actions: use repository or organization secrets, not hardcoded values in workflow files.
- Supabase: use Vault for server-side secrets, never expose `service_role` key to client-side code.
- n8n: use credential stores, not inline credentials in workflow JSON.
- Claude API: `ANTHROPIC_API_KEY` in environment variables only.

## Anti-patterns to Reject

- API keys in `.ts`/`.js`/`.py` files, even if "just for testing"
- Secrets in Docker build args (they persist in image layers)
- Shared credentials between dev and production
- Long-lived tokens with no expiry and no rotation schedule
- `console.log(config)` that dumps credentials to stdout
