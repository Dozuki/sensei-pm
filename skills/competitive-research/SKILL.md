---
name: competitive-research
description: Research and brief on connected-worker/manufacturing competitors (Poka, DeepHow, Augmentir, Intellect-Zaptic, Intertek Alchemy, VKS, Acadia, Parsable, SwipeGuide/L2L, Squint, QAD Redzone) using Dozuki's Notion Competitors database as the source of truth, then fill gaps with live web research and recent market news. Use whenever anyone on the team asks for a competitive brief, wants an update on a specific competitor, names a competitor from the database, or is prepping board/GTM/battlecard materials. Also trigger on "competitive research," "competitive intel," "who's in our competitor list," or requests for connected-worker market news.
---

# Competitor Research

Turns Dozuki's Notion Competitors database into a real, current competitive brief — not a hallucinated one. The database is the anchor; the web fills in what's stale or missing.

## Source of truth

Notion database: **🥊 Competitors** (`collection://95a7e82a-f643-4631-af0e-ea5c29582aa8`)

Schema:
| Field | Type | Notes |
|---|---|---|
| Company | title | |
| Competitive Rank | number | Lower = more direct threat. Not every row has one. |
| Summary | text | **Currently empty on every row as of last check** — don't assume it's populated. If it has content, treat it as the prior analysis to update, not ground truth to repeat verbatim. |
| userDefined:URL | url | Competitor's website |
| Added / Added By | created_time / created_by | System fields, read-only |

Known rows (ranked): 1 Poka, 2 DeepHow, 3 Augmentir, 4 Intellect-Zaptic, 5 Intertek Alchemy, 6 VKS. Unranked: Acadia, Parsable, SwipeGuide/L2L, Squint, QAD Redzone. Re-query rather than trusting this list blindly — it changes.

## Workflow

1. **Pull the row(s).** Query the data source directly rather than guessing:
   ```
   SELECT * FROM "collection://95a7e82a-f643-4631-af0e-ea5c29582aa8" WHERE "Company" LIKE '%<name>%'
   ```
   For a full landscape scan, pull all rows ordered by Competitive Rank.

2. **Check the individual page.** Each company row is also a Notion page (fetch its `url`) — some have supplementary content (demo video links, screenshots) beyond the table fields. Worth a quick check before assuming the table is all there is.

3. **Fill gaps with web research.** Since Summary is typically blank, this is where the actual work happens. Search for: current product positioning/messaging, pricing tier or packaging changes, recent funding or leadership news, and — especially — how they're pitching AI/agentic capabilities. (Prior research found Poka, DeepHow, Augmentir, and Squint have all converged on "agentic/MCP" vocabulary — check whether that's still their framing or if it's shifted.)

4. **Scan recent news — company-level and market-level.** Run both:
   - *Company-specific:* press releases, product launch announcements, funding rounds, leadership changes, partnership news. Search `"[Company] press release"` and `"[Company] news [current year]"` separately — press releases and third-party coverage surface differently.
   - *Market-level:* analyst coverage of the connected worker / frontline worker software category — Gartner, Forrester, IDC, LNS Research — plus trade press (IndustryWeek, Manufacturing.net, Automation World). Search things like `"connected worker platform" analyst report`, `"frontline worker software" market`, and `manufacturing connected worker Gartner`. This catches category-wide shifts (market sizing, consolidation, new entrants) that a single-company search misses.
   - Flag anything time-sensitive with a date so staleness is obvious later.

5. **Map against Dozuki's four platform layers** (Knowledge, Operations, Skills & Training, Insights) to pinpoint exactly where the competitor overlaps, where they're stronger, and where there's a real gap — not a vague "they compete with us."

6. **Output the brief** (format below).

7. **Offer to write back.** Ask before doing it, but offer to update the Notion Summary field with the synthesized findings via `notion-update-page` so the database stops being empty. Don't do this silently.

## Output format

```markdown
# [Company] — Competitive Brief
**Rank:** [N or "unranked"] · **URL:** [link] · **Last researched:** [date]

## Snapshot
2-3 sentences: what they sell, who they sell to, how they're funded/positioned.

## Platform overlap
| Dozuki Layer | Their coverage | Verdict |
|---|---|---|
| Knowledge | ... | Overlap / Gap / N/A |
| Operations | ... | |
| Skills & Training | ... | |
| Insights | ... | |

## Strengths (real, not generic)
## Gaps / weaknesses

## Recent News & Market Coverage
**Company-specific** (with dates):
- [Press release / news item] — [date] — [1-line takeaway]

**Market-level** (analyst & trade press on the connected worker category):
- [Report/article, source, date] — [1-line takeaway on how it affects competitive positioning]

## Counter-narrative angle
Where Dozuki's Trusted Data Loop / operational-data-network positioning creates real separation — only if it genuinely applies, not forced.
```

## Edge cases

- **Competitor not in the database:** confirm with the requester before adding, then create the page with matching schema (Company, URL, Competitive Rank if known) rather than leaving it orphaned.
- **Name doesn't match exactly** (e.g. "Zaptic" vs. "Intellect - Zaptic"): use `LIKE` matching, not exact string equality — several entries are compound names.
- **Multiple competitors requested at once:** run them as separate briefs, don't collapse into one table — rank and positioning nuance gets lost that way.