---
name: Three-Layer Protocol Stack for Multi-System AI Architectures
description: MCP (tool access) + A2A (agent-to-agent) + WebMCP (web interaction) — 100+ enterprises adopted by Feb 2026
type: insight
domain: ai_and_agents
source: Multiple — IBM, Oracle, Google, AWS, Anthropic, Salesforce, SAP (2026)
confidence: medium-high
date_added: 2026-04-08
date_verified: 2026-04-08
tags: [mcp, a2a, protocol-stack, enterprise-ai, interoperability]
related: [mcp_roadmap_aware_architecture.md, agentic_workflows_patterns.md]
---

## Core Principle

Interoperable enterprise AI deployments have converged on a three-layer architecture:

1. **MCP** — governs how agents access tools, data, and enterprise systems
2. **A2A** — governs how agents communicate with each other across departments, vendors, and organizations
3. **WebMCP** — governs how agents interact with the web

The Hierarchical Supervisor Pattern orchestrates above these layers.

## Evidence

- 100+ enterprises formally adopted this three-layer stack by February 2026
- IBM's ACP protocol was merged into A2A (August 2025)
- Oracle, Google, AWS, Anthropic, Salesforce, SAP all operate within this framework
- Notch (insurer-turned-AI-OS, 12x ARR, $30M Series A, March 25 2026) built on this stack
- Agency (Series A, November 2025) built on this stack

## When to Apply

Architecting any multi-system AI OS (agency, enterprise, or product). Evaluating whether a vendor's AI agent solution will integrate into a broader architecture without lock-in.

## Boundaries

Internal-only single-vendor tools with no cross-system integration needs do not require A2A. MCP alone is sufficient for tool access in bounded single-agent implementations.
