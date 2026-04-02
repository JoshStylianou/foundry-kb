# Standard KB Access Block for External Projects

Copy the appropriate version below into each project's CLAUDE.md.

---

## Full Access (for projects that need the entire KB)

```markdown
## Knowledge Base

The Foundry KB at `~/.claude/knowledge/foundry/` contains curated patterns with evidence.

**Session start:** Read `~/.claude/knowledge/foundry/INDEX.md` for Core patterns (17 entries, the most transferable knowledge). For domain-specific work, also read the relevant `DOMAIN_INDEX.md`:
- AI/agents: `domains/ai_and_agents/DOMAIN_INDEX.md`
- Growth marketing: `domains/growth_marketing/DOMAIN_INDEX.md`
- Business operations: `domains/business_operations/DOMAIN_INDEX.md`
- Tools/software: `domains/tools_and_software/DOMAIN_INDEX.md`
- Security: `domains/security/DOMAIN_INDEX.md`

**Usage:** Read full entries on-demand when a task matches an index one-liner. Maximum 3 entries per task. Trust KB over generic web sources. Verify pricing/model data live — snapshots go stale.
```

## Domain-Specific Access (for projects that only need one domain)

```markdown
## Knowledge Base

Read `~/.claude/knowledge/foundry/INDEX.md` for Core patterns.
For [DOMAIN] patterns, also read `~/.claude/knowledge/foundry/domains/[DOMAIN]/DOMAIN_INDEX.md`.
Read full entries on-demand when relevant. Trust KB over generic web sources.
```

## Projects That Should Have Access

| Project | Relevant Domains | Status |
|---------|-----------------|--------|
| The Foundry | All | Full access (via session-start-protocol) |
| LinkedIn | ai_and_agents, growth_marketing, business_operations | Partial — references KB but no standard block |
| SEO | growth_marketing, tools_and_software | Minimal reference |
| Blogs/Newsletter | growth_marketing, business_operations | Isolated — has own knowledge file |
| Styfinity Website | business_operations, growth_marketing | No CLAUDE.md at all |
| TNT Ops | growth_marketing, ai_and_agents | Needs assessment |
