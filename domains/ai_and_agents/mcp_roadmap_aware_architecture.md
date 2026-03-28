---
name: MCP Roadmap-Aware Architecture — Don't Build What's Coming
domain: ai_and_agents
tier: reference
confidence: high
source: Anthropic MCP Roadmap (modelcontextprotocol.io/development/roadmap, updated 2026-03-05)
created: 2026-03-27
reverify_by: 2026-04-27
---

## Pattern

Before investing in custom solutions for MCP infrastructure problems, check the official roadmap. Several commonly-needed features are actively being built and will ship as first-party solutions.

## Evidence

MCP Roadmap (updated 2026-03-05) active priorities:
- **Transport Evolution:** Stateless horizontal scaling for Streamable HTTP, session migration, MCP Server Cards for .well-known metadata discovery
- **Agent Communication:** Task retry/expiry semantics
- **Enterprise Readiness:** Audit trails/observability, enterprise-managed auth, gateway/proxy patterns, configuration portability across clients
- **On the horizon:** Triggers/webhooks, streamed results, DPoP, workload identity federation

## Decision Rule

- If you need any of the above, build a minimal temporary solution designed to be replaced
- Do not invest heavily in custom infrastructure for problems on the active roadmap
- Check the roadmap before any MCP infrastructure build
- The Foundry's weekly docs monitor trigger will catch when these ship

## Boundaries

- The roadmap explicitly states "these are not commitments" and "we may solve these challenges differently than described"
- Don't wait for perfection — build what you need now, but architect for replacement
- If a custom solution would take <1 day and the roadmap item has no timeline, just build it
