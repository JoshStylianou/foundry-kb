---
name: Lethal Trifecta — Three-Condition AI Agent Security Vulnerability
domain: security
tier: reference
confidence: high
source: Simon Willison (simonw.substack.com/p/the-lethal-trifecta-for-ai-agents + Lenny's Apr 2, 2026)
created: 2026-04-05
reverify_by: 2026-07-05
tags: [agent-security, prompt-injection, architectural-separation, threat-model]
---

## Pattern

Any agent combining three conditions is inherently exploitable via prompt injection — regardless of model quality:
1. **Private data access** — reads confidential information
2. **Untrusted external content exposure** — processes content from outside the trust boundary
3. **Ability to communicate externally** — can take outbound actions (email, API calls, messages)

Removing any single leg eliminates the vulnerability class entirely. Analogized to Challenger disaster failure conditions — each individually acceptable, catastrophic in combination.

## Decision Rule

When architecting any agent, check for the trifecta. If all three conditions are present, the design is exploitable. Mitigate by removing one leg:
- Remove external content → agent only processes internal data
- Remove outbound actions → agent can read external content but can't act on injection
- Remove private data → agent can act externally but has nothing sensitive to leak

## Boundaries

- Architectural separation is the fix — model quality cannot solve it
- This is a vulnerability *class*, not a specific exploit — no amount of prompt hardening eliminates it when all three legs are present
- Some high-value agents genuinely need all three conditions — in these cases, human-in-the-loop approval on outbound actions is the minimum viable mitigation
