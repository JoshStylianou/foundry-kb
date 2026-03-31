---
title: Vercel Domain Verification Blockers — Account Claims and TXT Code Rotation
domain: tools_and_software
type: lesson
source: josh_input
confidence: high
date_added: 2026-03-31
date_verified: 2026-03-31
tags: vercel, dns, domain, deployment, troubleshooting
related: []
---

## Lesson 1: "Verification Needed" = Domain Claimed on Another Vercel Account

When Vercel shows "Verification Needed" on a custom domain and all DNS records (A, CNAME, TXT) are correct and propagated, the blocker is almost always that the domain is claimed on a **different Vercel account or project**. No amount of DNS debugging will fix it — the other account must release the domain first.

**Diagnostic sequence:**
1. Verify DNS records are correct and propagated (nslookup against 8.8.8.8)
2. If DNS is correct but verification still fails → ask: "Is this domain added to any other Vercel project or account?"
3. Get the other account holder to remove the domain from their project (Settings → Domains → Remove)
4. Then refresh or re-add on your side

## Lesson 2: Re-Adding a Domain Generates a New TXT Verification Code

When you remove a domain from a Vercel project and re-add it, Vercel generates a **completely new** `_vercel` TXT verification value. The old TXT record in DNS becomes stale and verification will fail silently until you update it.

**After any remove/re-add:**
1. Copy the new TXT value from Vercel's domain settings
2. Update the `_vercel` TXT record at your DNS provider
3. Wait for propagation (or check with `nslookup -type=TXT _vercel.yourdomain.com 8.8.8.8`)
4. Hit Refresh on Vercel

## Evidence
Direct experience deploying styfinity.com (2026-03-31). Domain was stuck on "Verification Needed" for 15+ hours with correct DNS. Root cause: contractor (James) had styfinity.com on his Vercel account. After he released it, re-adding generated a new TXT code that also needed updating.

## Why This Matters
Saves hours of misdiagnosed DNS debugging on any future Vercel deployment where domains are being transferred between accounts or projects.

## Action Triggers
- Any Vercel domain showing "Verification Needed" despite correct DNS
- Migrating a domain from one Vercel account/project to another
- Taking over a domain from a contractor or agency's Vercel setup
