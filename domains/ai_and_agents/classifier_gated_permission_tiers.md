---
name: Classifier-gated permission tiers eliminate binary autonomy tradeoffs
description: Three-tier permission structure (whitelist / conditional / classifier-gated) lets agents act autonomously without full bypass risk. 0.4% false positive, 5.7% false negative on exfiltration attempts.
domain: ai_and_agents
source: Anthropic (Claude Code Auto Mode, March 24 2026), TechCrunch, Help Net Security, Nate Herk
confidence: medium-high
date_added: 2026-03-26
date_verified: 2026-03-26
tags: [agent-safety, permissions, autonomous-execution, classification, security, tiered-access]
related: [agentic_workflows_patterns.md, consulting_agent_architecture.md]
---

## Pattern

When AI agents need autonomous execution, structuring action authorization as tiered permission layers eliminates the binary "always ask / never ask" tradeoff. Three tiers: a whitelist of always-safe operations (reads, navigation), a conditional layer for in-scope writes (project files, git), and a gated layer (bash execution, external calls, destructive operations) that requires classifier review before proceeding. The classifier evaluates at multiple checkpoints — spawn, mid-execution, and return — catching compromised subagents, not just bad initial requests.

## Evidence

- Claude Code Auto Mode launched March 24, 2026 as research preview (Team plan, Sonnet 4.6 and Opus 4.6)
- Internal testing: 0.4% false positive rate, 5.7% false negative rate on synthetic exfiltration attempts
- Three-tier structure validated: Tier 1 (always allow), Tier 2 (conditional allow within project scope), Tier 3 (classifier review per action)
- Subagents evaluated at spawn, mid-execution, and on return — flags if a subagent was compromised by content it read during execution
- Activation: `claude --enable-auto-mode` or Shift+Tab in interactive mode
- Sources: TechCrunch, Help Net Security, Anthropic release notes, Nate Herk (@nateherk) "STOP Using Bypass Permissions, Use This New Feature Instead" (March 26, 2026)

## Application Trigger

Use this when designing any agent pipeline that needs autonomous execution without full bypass-permissions risk:
- AI coding agents that run bash commands, modify files, and call external APIs
- Automated workflow agents that interact with production systems
- Multi-agent systems where subagents may process untrusted content (web pages, user documents, external APIs)

The pattern is especially relevant when the alternative is binary: either interrupt the human on every action (kills flow) or bypass all checks (creates risk).

## Boundaries

- Classifier review adds latency per Tier-3 action — not suitable for real-time, sub-second agent loops
- Classifier criteria are not public — you cannot audit or customize what triggers gating
- Research preview only (Team plan) — not yet available on all plan tiers
- 5.7% false negative rate means ~1 in 18 genuinely dangerous actions may pass through — this is a safety layer, not a guarantee
- Does not replace input validation or output sandboxing — it's one layer in a defense-in-depth approach
