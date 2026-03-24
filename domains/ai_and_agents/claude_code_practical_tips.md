---
name: Claude Code Practical Tips
description: Hooks vs Skills vs Slash Commands, Gemini CLI fallback, verification tables, clipboard workflows
type: insight
domain: ai_and_agents
source: AI Learning Knowledge Base — YouTube transcripts
confidence: high
date_added: 2026-03-21
tags: [claude-code, tips, productivity, workflows]
related: [claude_code_advanced_workflows.md, claude_code_context_management.md]
---

## Hooks vs Skills vs Slash Commands

| Mechanism | Trigger | Structure | Token Cost | Best For |
|-----------|---------|-----------|------------|----------|
| **Slash commands** | Manual (`/command`) | Single .md file | Minimal | Quick actions the user explicitly invokes |
| **Skills** | Auto-triggered by Claude based on description match | Multiple files (skill.md + references/ + scripts/) | Medium-high (loads into context) | Complex workflows that should activate without user knowing the command |
| **Hooks** | Programmatic checks in settings.json | Code-based (no LLM involved) | Zero LLM tokens | Guardrails, banned word checks, format enforcement — anything rule-based |

**Key insight on hooks:** They run without consuming LLM tokens. Use hooks for anything that can be expressed as a deterministic rule (regex, word list, format check). Reserve skills for things that require judgment.

## Gemini CLI as Fallback

Some sites block Claude's web fetching (Reddit, paywalled content). **Gemini CLI can access these.** Use it as a fallback tool when Claude's native web access fails on specific domains.

## "Last 30 Days" Skill Pattern

A skill that scans Reddit and X for trending research in the past 30 days on a given topic. Useful for staying current without manual browsing. Feeds into the research pipeline.

## Clipboard Workflow for LinkedIn

Copy output to clipboard rather than writing to file when the destination is LinkedIn. LinkedIn's editor strips markdown formatting from pasted file content, but clipboard-native text preserves the intended formatting.

## Verification Tables

When making factual claims (statistics, dates, attributions), **always produce a verification table** with:
- Claim
- Source
- Confidence level
- Verification status

This catches hallucinated statistics before they reach publication. Non-negotiable for any content that will be published externally.
