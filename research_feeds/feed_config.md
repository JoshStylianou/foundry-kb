# Foundry Research Feed Configuration

**Last updated:** 2026-03-21
**Maintained by:** kb-curator agent
**Research cadence:** Daily

---

## Instructions for kb-curator

This file defines what The Foundry researches every day autonomously. Update it when:
- A new project starts (add relevant topics)
- A project ends (retire or reduce topics)
- Josh's inputs signal a new area of interest
- A topic has been exhausted (no new signal for 14 days)

---

## Active Topics

### 1. AI Agent Architectures & Self-Improving Systems
**Why:** The Foundry's primary improvement vector. We need to know what the best practitioners are building.
**Search strategy:**
- Latest releases: LangChain, CrewAI, AutoGen, Claude agent SDK updates
- Practitioner posts on agent memory, tool use, multi-agent coordination
- Academic papers on agent self-improvement, knowledge accumulation
**Signal threshold:** Only log if it changes how The Foundry is architected or run
**Domain:** `ai_and_agents`

### 2. Performance Marketing Signals
**Why:** TNT Growth — 60 clients, ~$480K MRR. Any signal that affects paid media strategy affects Josh's core contracted revenue.
**Search strategy:**
- Meta/Google Ads algorithm updates and best practices
- Agency operating models — what high-margin agencies are doing differently
- AI in paid media — tools, automation, what's working at scale
**Signal threshold:** Only log if it would change a client recommendation or agency operation
**Domain:** `growth_marketing`

### 3. Forex & AI Trading Signals
**Why:** TraiderJ — AI-powered forex signals via WhatsApp. Quality of signals is the product.
**Search strategy:**
- Major macro shifts affecting forex (central bank decisions, geopolitical events)
- AI trading tools and signal methodologies
- Practitioner forex analysis from credible sources (not retail noise)
**Signal threshold:** Only log if it would affect signal quality or TraiderJ's positioning
**Domain:** `forex_trading`

### 4. Claude API & Anthropic Platform Updates
**Why:** The Foundry is built on Claude. Any new capability is a direct upgrade opportunity.
**Search strategy:**
- Anthropic announcements, blog posts, changelog
- Claude API new features: tool use, extended context, new models
- Community practitioner reports on what works and what doesn't
**Signal threshold:** Any capability update or pricing change — always relevant
**Domain:** `ai_and_agents`

### 5. Business AI OS Implementations
**Why:** TNT Growth's AI OS initiative — targeting 80% gross margin. Knowing what others are building is competitive intelligence.
**Search strategy:**
- Agencies implementing AI operations at scale
- AI-first business operating systems — what gets automated first, what doesn't
- ROI reports on AI implementation in professional services
**Signal threshold:** Only log if it informs the TNT AI OS architecture or timeline
**Domain:** `business_operations`

---

## Retired Topics

*Moved here when a topic is no longer active.*

---

## Topic Addition Template

When adding a new topic, copy this template:

```markdown
### N. [Topic Name]
**Why:** [Which business/project this serves and why it matters]
**Search strategy:**
- [Specific source 1]
- [Specific source 2]
- [Specific source 3]
**Signal threshold:** [What makes something worth logging]
**Domain:** [domain folder name]
```
