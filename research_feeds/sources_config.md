# Foundry KB — Source Configuration

**Maintained by:** kb-curator
**Last updated:** 2026-03-21

---

## Primary Input Sources

### 1. AI Learning Knowledge Base (Google Doc)
**URL:** https://docs.google.com/document/d/1DphfHOgGvsVlmBCyFy4rsRwDFLPDHFD3YdnEupYO8ag/edit?tab=t.0
**Document ID:** `1DphfHOgGvsVlmBCyFy4rsRwDFLPDHFD3YdnEupYO8ag`
**MCP server:** `google-drive-tntgrowth`
**Content type:** YouTube video transcripts — Josh adds these manually
**Check frequency:** Every research cycle (daily)
**Last processed:** never
**Last known length:** 0 characters

**Processing instructions:**
- Read the full doc on each cycle
- Compare against `last known length` to detect new content
- Process only new content added since last run (do not re-process existing entries)
- Treat each transcript as a source — extract knowledge FROM it, do not store the raw transcript
- See kb-curator transcript processing protocol

---

## Source Addition Template

```markdown
### N. [Source Name]
**URL:** [full URL]
**Document ID:** [ID if applicable]
**MCP server:** [which MCP handles this]
**Content type:** [what kind of content]
**Check frequency:** [daily | weekly | on-demand]
**Last processed:** [date or never]
**Last known length:** [character count or 0]

**Processing instructions:**
[How to handle content from this source]
```
