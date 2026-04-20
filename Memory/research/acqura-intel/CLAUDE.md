# Acqura Intel Wiki — Operating Manual

> This file is the schema for the `acqura-intel` wiki. Read it at the start of every session that touches this wiki. It defines structure, conventions, and workflows. Follow it precisely — consistency is what makes the wiki useful over time.

---

## Purpose

This wiki is a persistent, compounding knowledge base on the **competitive landscape for paid media systems, growth platforms, and industry knowledge relevant to Acqura Growth OS**. It is Dennis's primary research artifact for Acqura product development.

**Scope:**
- Paid media platforms and tools (ad tech, attribution, audience targeting)
- Growth OS / Revenue Intelligence platforms (competitors and analogues to Acqura)
- Paid acquisition strategies and frameworks
- Account-based marketing (ABM), intent data, CDPs, data enrichment
- Key industry thinkers, practitioners, and their frameworks
- Market trends, analyst reports, ecosystem maps

**Out of scope:**
- Organic/SEO (unless it intersects with paid or the Growth OS concept)
- Eksido or Sam Siam operational content (those have their own vault paths)
- General Salesforce CRM content unless directly relevant to Acqura's positioning

---

## Directory Structure

```
Memory/research/acqura-intel/
├── CLAUDE.md          ← This file. Read first, every session.
├── index.md           ← Content catalog. Updated on every ingest.
├── log.md             ← Append-only activity log. Never delete entries.
├── raw/               ← Source documents. IMMUTABLE — read only, never edit.
│   └── assets/        ← Downloaded images from web clips.
└── wiki/
    ├── overview.md    ← Evolving synthesis / master thesis. Updated regularly.
    ├── entities/      ← One page per company, platform, or tool.
    ├── concepts/      ← One page per strategy, framework, tactic, or metric.
    ├── sources/       ← One page per ingested source (summary + key extracts).
    └── analyses/      ← Filed query outputs: comparisons, breakdowns, memos.
```

**Hard rule:** The LLM writes the `wiki/` layer. Dennis writes nothing in `wiki/` directly — all wiki content flows through ingest or query workflows below.

**Hard rule:** `raw/` is append-only. Never modify, rename, or delete raw sources.

---

## Page Formats

### Entity Page (`wiki/entities/<slug>.md`)

```markdown
---
name: <Company / Platform Name>
type: entity
category: <platform | tool | competitor | data-provider | agency>
tags: [<tag1>, <tag2>]
sources: <count of sources this page draws from>
last_updated: YYYY-MM-DD
---

# <Name>

## What It Is
One paragraph. What it does, who it serves, positioning.

## Relevance to Acqura
Why this matters for Acqura Growth OS — competitive threat, analogue, inspiration, or gap it reveals.

## Key Capabilities
- Bullet list of notable features or differentiators.

## Pricing / Business Model
What is known. Mark unknown as `[unknown]`.

## Strengths
- ...

## Weaknesses / Gaps
- ...

## Contradictions / Open Questions
- Any conflicts between sources, or things that need verification.

## Sources
- [[source-slug]] — one-line note on what it contributed
```

### Concept Page (`wiki/concepts/<slug>.md`)

```markdown
---
name: <Concept Name>
type: concept
category: <strategy | framework | tactic | metric | market-term>
tags: [<tag1>, <tag2>]
sources: <count>
last_updated: YYYY-MM-DD
---

# <Concept Name>

## Definition
Clear, concise definition. Avoid jargon unless defined here.

## Why It Matters for Acqura
Direct link to Acqura Growth OS / GTI framework — how this concept informs product decisions.

## How It Works
Mechanism, workflow, or mental model.

## Key Practitioners / Platforms
Who does this well. Link to entity pages where applicable.

## Acqura's Angle
How Acqura should position relative to this concept — adopt, adapt, counter, or differentiate.

## Contradictions / Open Questions
- ...

## Sources
- [[source-slug]] — one-line note
```

### Source Page (`wiki/sources/<slug>.md`)

```markdown
---
title: <Original Title>
type: source
format: <article | youtube | podcast | report | book | thread>
url: <original URL or file path>
author: <author or channel name>
date_published: YYYY-MM-DD
date_ingested: YYYY-MM-DD
tags: [<tag1>, <tag2>]
---

# <Title>

## Summary
3-5 sentences. Core argument or content. What makes this source worth keeping.

## Key Takeaways
- Bullet list of the most important points — claims, data, frameworks, quotes.

## Notable Quotes / Data Points
> "Direct quote if striking."

- Any statistics, numbers, or specific claims worth citing.

## Wiki Pages Updated
List every wiki page touched during this ingest:
- [[entity-slug]] — what was added/changed
- [[concept-slug]] — what was added/changed

## Gaps / Follow-up
- What this source raised but didn't answer.
- Suggested follow-up sources or searches.
```

### Analysis Page (`wiki/analyses/<slug>.md`)

```markdown
---
title: <Analysis Title>
type: analysis
question: <The question this analysis answers>
date: YYYY-MM-DD
tags: [<tag1>, <tag2>]
---

# <Title>

## Question
The exact question this was filed to answer.

## Answer
Direct answer, up front.

## Supporting Evidence
Organized by sub-question or theme. Cite source pages.

## Limitations
What's missing, uncertain, or based on thin evidence.

## Implications for Acqura
Specific product, positioning, or strategy implications.
```

---

## Workflows

### Ingest Workflow

Triggered when Dennis drops a new source into `raw/` and says "ingest [filename]" or "ingest this."

**Step 1 — Read the source.**
Read the raw file fully. If it contains images, note the image paths and read key ones separately.

**Step 2 — Discuss.**
Surface 3-5 key takeaways and ask Dennis: "Anything here you want to emphasize or de-emphasize before I file it?"

**Step 3 — Write the source page.**
Create `wiki/sources/<slug>.md` using the source page format. Slug = kebab-case of the title.

**Step 4 — Update entity and concept pages.**
For every company, platform, tool, strategy, or framework mentioned significantly in the source:
- If the page exists: update it. Add new information, note contradictions, update `sources` count and `last_updated`.
- If the page doesn't exist: create it using the appropriate template.

**Step 5 — Update overview.md.**
If the source shifts the overall picture — adds a new player, challenges a previous claim, introduces a new concept — update `wiki/overview.md` accordingly.

**Step 6 — Update index.md.**
Add the new source page. Update entity/concept pages if they were created (not just updated).

**Step 7 — Append to log.md.**
Format: `## [YYYY-MM-DD] ingest | <Source Title>`
Include: source type, pages created, pages updated, one-line synthesis note.

**Typical surface area:** 1 source → 1 source page + 3-8 entity/concept page updates.

---

### Query Workflow

Triggered when Dennis asks a question against the wiki.

**Step 1 — Read index.md** to find relevant pages.

**Step 2 — Read relevant pages** (source, entity, concept as needed).

**Step 3 — Synthesize and answer.** Lead with the direct answer. Cite pages. Flag uncertainty.

**Step 4 — Offer to file.** If the answer is non-trivial (a comparison, a competitive breakdown, a strategic analysis), offer: "Want me to file this as an analysis page?" If yes, write `wiki/analyses/<slug>.md` and append to log.md.

---

### Lint Workflow

Triggered by Dennis saying "lint the wiki" or periodically suggested after every 10 ingests.

Check for:
- Pages with no inbound links (orphans)
- Entity pages with `[unknown]` fields that newer sources could fill
- Contradictions between pages that haven't been resolved
- Concepts mentioned in source pages but lacking their own concept page
- Claims in overview.md superseded by newer sources
- Missing cross-references (entity mentions concept but no `[[link]]`)

Output: a lint report in chat. Offer to file it as `wiki/analyses/lint-YYYY-MM-DD.md` if useful.

---

## Index Conventions

`index.md` is organized into four sections: Sources, Entities, Concepts, Analyses.

Each entry: `| [[slug]] | One-line description | YYYY-MM-DD |`

The index is the LLM's navigation tool — keep descriptions specific enough to be useful at a glance.

---

## Log Conventions

`log.md` is append-only. Never edit or delete past entries.

Entry header format: `## [YYYY-MM-DD] <type> | <Title>`
Types: `ingest`, `query`, `lint`, `analysis`

Each entry includes: what happened, what changed, one-line synthesis note.

Grep-friendly: `grep "^## \[" Memory/research/acqura-intel/log.md` returns all entries in order.

---

## Cross-Referencing Rules

- Use Obsidian wikilinks: `[[slug]]` for pages within this wiki.
- Always link entity and concept names on first mention in a page — don't repeat links within the same page.
- Source pages link to the entities/concepts they update. Entity/concept pages list their sources. This bidirectional linking is what makes the wiki navigable.

---

## Overview.md Conventions

`wiki/overview.md` is the master synthesis — the evolving answer to: *"What do I know about the competitive landscape for paid media systems and growth OS platforms, and what does it mean for Acqura?"*

It is not an index. It is a living memo. It should:
- Lead with the current thesis (2-3 sentences on the landscape)
- Organize key insight clusters
- Flag open questions and gaps
- Note where the picture is still thin

Update it on every ingest that meaningfully shifts the thesis. Small sources that confirm existing knowledge may not require an update.

---

## Naming Conventions

- Slugs: `kebab-case`, lowercase, no special characters
- Entity slugs: company name (`triple-whale`, `northbeam`, `6sense`)
- Concept slugs: concept name (`intent-data`, `multi-touch-attribution`, `growth-os`)
- Source slugs: abbreviated title (`yt-triple-whale-attribution-2024`, `article-hubspot-abm-guide`)
- Analysis slugs: descriptive + date (`competitor-comparison-attribution-2026-04`)

---

## Session Start Protocol

At the start of any session touching this wiki:
1. Read `CLAUDE.md` (this file)
2. Read `index.md` to understand current wiki state
3. Read the last 3 entries in `log.md` for recent context
4. Read `wiki/overview.md` for current thesis

Then proceed with the session task.
