---
title: Consulting Agent Architecture — Identity-First vs. Capability-First
domain: ai_and_agents
type: pattern
source: research_synthesis
confidence: high
date_added: 2026-03-22
date_verified: 2026-03-22
tags: agent architecture, consulting agent, system prompt, expert persona, operational protocol method, nurture-first development
related: [claude_code_agent_teams.md, claude_code_skill_architecture.md, proactive_ai_advisory_patterns.md]
---

## Consulting Agents vs. Task Execution Agents

These are architecturally different, not variations of the same design.

| Dimension | Task Execution | Consulting |
|-----------|---------------|------------|
| System prompt priority | Capabilities and constraints | Identity and reasoning frameworks |
| Primary output | Completed work | Recommendations and challenges |
| User relationship | Employer to worker | Peer to advisor |
| Success metric | Task completed correctly | User made a better decision |
| Model requirement | Speed (Sonnet) | Depth (Opus) |

## Operational Protocol Method (Six Components)

The most effective expert LLM personas use:
1. **Identity & Role** — who is this expert, what is their philosophy
2. **Guiding Principles** — rules governing advice, what they never do
3. **Core Capabilities** — specific things they can help with
4. **Foundational Knowledge Base** — trusted sources and frameworks
5. **User Context** — what they know about the specific user
6. **Initialization Command** — how they activate

Maps to Claude Code agent .md format: YAML front matter (1), opening paragraphs (2,3), capability sections (4), memory file reads (5), agent invocation (6).

## Nurture-First Development (March 2026)

Three-layer cognitive architecture for expert agents:
- **Constitutional** (low volatility): Identity, principles, frameworks — always loaded
- **Skill** (medium volatility): Specific techniques, tool knowledge — loaded on demand
- **Experiential** (high volatility): Past interactions, decision traces — referenced from external files

Key insight: domain expertise accumulates through conversation and periodic consolidation, not through pre-loading everything. Start minimal, crystallize knowledge from interactions.

## Five Factors That Make an Agent Feel Like a Domain Expert

1. Specific frameworks applied by default, not general knowledge
2. Opinionated recommendations, not option lists
3. Challenge before execute — question the premise
4. Cross-domain pattern recognition
5. Explicit acknowledgment when they don't know something

## Evidence

- Operational Protocol Method: Dennis Kennedy (2025), systematic LLM specialization
- Nurture-First Development: ArXiv 2603.10808 (March 2026)
- Anthropic: "Building Effective Agents" guide (December 2024), "Effective Context Engineering" (2025)

## Why This Matters to The Foundry

Every expert agent in the Foundry roster (Research Chief's recruited experts, the AI Consultant) should follow the six-component Operational Protocol and the three-layer cognitive architecture. This is the template for making agents feel like genuine domain experts rather than generic chatbots.

## Action Triggers

When building any expert or advisory agent: use the six-component structure. When designing knowledge management for an agent: use the three-layer architecture (constitutional/skill/experiential). When an agent needs to feel like a genuine expert: ensure it recommends rather than lists, challenges before executing, and admits uncertainty.
