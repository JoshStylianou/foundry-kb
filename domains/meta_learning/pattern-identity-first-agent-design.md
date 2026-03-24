---
title: Identity-First Agent Prompt Design
domain: meta_learning
type: pattern
source: ai_consultant_agent_architecture
confidence: high
date_added: 2026-03-22
date_verified: 2026-03-22
tags: agent design, system prompts, consulting agents, identity-first, prompt architecture
related: [consulting_agent_architecture.md, proactive_ai_advisory_patterns.md]
---

## The Pattern

When designing agents whose value comes from judgment (not task execution), the system prompt must be identity-first, not capability-first. The first ~30 lines define WHO the agent is and HOW it thinks. Capabilities, tools, and procedures come after identity.

**Identity-first prompt structure:**
1. Character definition (who you are, how you think)
2. Behavioral principles (what you always do, what you never do)
3. Methodology (how you approach problems)
4. Knowledge access (where to find information)
5. Integration points (how you connect to other systems)

**Capability-first prompt structure (anti-pattern for judgment agents):**
1. Tools and capabilities
2. Procedures and workflows
3. Constraints and rules
4. User context

## Why This Matters

Identity-first prompts produce fundamentally different model behavior than capability-first prompts. When the model's first instructions define a character with expertise and opinions, it reasons from that character. When the first instructions define capabilities and rules, the model optimizes for rule-following, which produces helpful but unchallenging output.

The difference is measurable: identity-first prompts produce genuine pushback and recommendations. Capability-first prompts produce option lists and deference.

## Evidence

- Operational Protocol Method (Dennis Kennedy 2025): Identity & Role is component 1 of 6 because it governs interpretation of all other components
- Five factors for expert agent feel: 4 of 5 are judgment-based (frameworks, opinions, challenge, limits), only 1 is knowledge-based
- Validated in the AI Consultant Agent architecture (March 2026): identity layer governs the model's entire behavioral posture

## Why This Matters to The Foundry

Every advisory or consulting agent in the Foundry should use identity-first prompt design. Task execution agents (Builder) can remain capability-first. This distinction determines whether an agent behaves as a thinking partner or a task processor.

## Action Triggers

- When designing any new agent whose primary value is judgment, analysis, or advisory (not code generation or task completion), use identity-first prompt structure
- When an existing agent is producing "helpful but unchallenging" output, check whether its prompt is capability-first and consider restructuring
- When the system prompt exceeds ~200 lines, the identity layer risks dilution -- keep it under 200 lines total with identity in the first 30-35 lines
