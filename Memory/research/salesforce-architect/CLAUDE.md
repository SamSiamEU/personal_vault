# Salesforce Architect Wiki — Operating Manual

> This file is the schema for the `salesforce-architect` wiki. Read it at the start of every session that touches this wiki. It defines structure, conventions, and workflows. Follow it precisely — consistency is what makes the wiki useful over time.

---

## Purpose

This wiki is a persistent, compounding knowledge base on **Salesforce architecture** — capturing both Dennis's own intellectual property and curated external references. It is Dennis's primary artifact for Salesforce solution design, client delivery, and thought leadership.

**Two knowledge types — treat them differently:**

1. **Own IP** (`wiki/solutions/`) — Dennis's past solutions, architecture decisions, client presentations, and frameworks he has built. This is proprietary. Source of truth is Dennis's direct input. The LLM helps structure and cross-reference it, but never invents or dilutes it.
2. **External references** (`wiki/entities/`, `wiki/concepts/`, `wiki/sources/`) — Salesforce official docs, open source tools, community best practices, Trailhead content, partner ecosystem knowledge.

**Scope:**
- Salesforce platform architecture (Sales Cloud, Service Cloud, Experience Cloud, Data Cloud, Agentforce)
- Integration patterns (MuleSoft, direct API, CDC, Platform Events, Pub/Sub)
- Data architecture (Salesforce data model, big objects, external objects, Einstein features)
- DevOps and release management (SFDX, Salesforce DX, CI/CD, scratch orgs)
- Governance, security, and compliance patterns
- CPQ, Revenue Cloud, Field Service Lightning
- Industry clouds (Financial Services, Health, Manufacturing)
- Partner ecosystem tools (Copado, Gearset, Flosum, OwnBackup, etc.)
- Dennis's client frameworks, accelerators, and reusable patterns
- Community resources: Salesforce Ben, Andy in the Cloud, unofficial Slack, Ohana

**Out of scope:**
- General CRM strategy unless tied to Salesforce implementation
- Acqura or Eksido operational content (those have their own vault paths)
- Non-Salesforce technology unless it's in direct integration with Salesforce

---

## Directory Structure

```
Memory/research/salesforce-architect/
├── CLAUDE.md          ← This file. Read first, every session.
├── index.md           ← Content catalog. Updated on every ingest.
├── log.md             ← Append-only activity log. Never delete entries.
├── raw/               ← Source documents. IMMUTABLE — read only, never edit.
│   └── assets/        ← Downloaded images, diagrams, screenshots.
└── wiki/
    ├── overview.md    ← Evolving synthesis / master thesis. Updated regularly.
    ├── entities/      ← One page per platform, tool, cloud, or ecosystem player.
    ├── concepts/      ← One page per pattern, framework, tactic, or Salesforce-specific term.
    ├── solutions/     ← Dennis's own IP: past solutions, decisions, frameworks, accelerators.
    ├── sources/       ← One page per ingested external source (summary + key extracts).
    └── analyses/      ← Filed query outputs: comparisons, breakdowns, architecture memos.
```

**Hard rule:** The LLM writes the `wiki/` layer for external knowledge. For `wiki/solutions/`, Dennis provides the raw input — the LLM structures, formats, and cross-references it, but never fabricates solution content.

**Hard rule:** `raw/` is append-only. Never modify, rename, or delete raw sources.

---

## Page Formats

### Solution Page (`wiki/solutions/<slug>.md`)

This is for Dennis's own IP only. Do not create solution pages from external sources.

```markdown
---
name: <Solution / Framework / Decision Name>
type: solution
category: <architecture | integration | data | devops | governance | framework | accelerator | presentation>
client: <client name or "generic" if reusable>
date: YYYY-MM-DD
tags: [<tag1>, <tag2>]
status: <draft | active | deprecated>
---

# <Solution Name>

## Context
What problem this was solving. Client situation, constraints, or use case.

## Decision / Approach
The architecture or solution chosen. Be specific — include component names, integration methods, data flows.

## Rationale
Why this approach over alternatives. Key trade-offs made.

## Key Components
- Bullet list of Salesforce components, integrations, or custom build involved.

## Reusability
How this pattern could apply to other clients or contexts. What to parameterize.

## Lessons Learned
What worked. What didn't. What to do differently next time.

## Related Pages
- [[concept-slug]] — how this solution implements or extends the concept
- [[entity-slug]] — tools or platforms involved
- [[solution-slug]] — related solutions
```

### Entity Page (`wiki/entities/<slug>.md`)

```markdown
---
name: <Platform / Tool / Cloud Name>
type: entity
category: <salesforce-cloud | integration-tool | devops-tool | data-tool | partner-app | community-resource>
tags: [<tag1>, <tag2>]
sources: <count of sources this page draws from>
last_updated: YYYY-MM-DD
---

# <Name>

## What It Is
One paragraph. What it does, who it serves, positioning within the Salesforce ecosystem.

## Relevance to Architecture Work
Why this matters — when to recommend it, when to avoid it, key architectural considerations.

## Key Capabilities
- Bullet list of notable features or differentiators.

## Licensing / Pricing
What is known. Mark unknown as `[unknown]`.

## Strengths
- ...

## Weaknesses / Gaps
- ...

## Known Gotchas
- Limits, quirks, governor limits, or integration constraints worth flagging.

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
category: <architecture-pattern | integration-pattern | data-pattern | devops-pattern | governance | salesforce-term>
tags: [<tag1>, <tag2>]
sources: <count>
last_updated: YYYY-MM-DD
---

# <Concept Name>

## Definition
Clear, concise definition. Avoid jargon unless defined here.

## When to Use
Scenarios and use cases where this pattern applies.

## How It Works
Mechanism, workflow, or mental model. Include Salesforce-specific implementation details.

## Key Constraints
- Governor limits, platform restrictions, or architectural trade-offs.

## Related Patterns / Alternatives
Competing or complementary patterns. When to choose this vs. alternatives.

## Dennis's Take
How Dennis applies or adapts this concept in practice. Personal perspective on best practices.

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
format: <article | youtube | trailhead | docs | podcast | report | book | thread>
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
Organized by sub-question or theme. Cite source pages and solution pages.

## Limitations
What's missing, uncertain, or based on thin evidence.

## Architecture Implications
Specific design, recommendation, or delivery implications.
```

---

## Workflows

### Own IP Ingest Workflow

Triggered when Dennis describes a past solution, decision, framework, or client deliverable.

**Step 1 — Listen and clarify.**
Ask for any missing context: client situation, constraints, what was decided, why.

**Step 2 — Discuss.**
Reflect back the key architectural decisions and ask: "Anything to emphasize or clarify before I file it?"

**Step 3 — Write the solution page.**
Create `wiki/solutions/<slug>.md` using the solution page format. Slug = kebab-case descriptor.

**Step 4 — Cross-reference.**
Link to relevant entity and concept pages. If a new concept emerges that doesn't have a page, create it.

**Step 5 — Update index.md.**
Add the solution page. Update entity/concept pages if created.

**Step 6 — Append to log.md.**
Format: `## [YYYY-MM-DD] ingest | <Solution Name>`
Include: category, client context, pages created, pages updated, one-line synthesis note.

---

### External Source Ingest Workflow

Triggered when Dennis drops a new source into `raw/` and says "ingest [filename]" or "ingest this."

**Step 1 — Read the source.**
Read the raw file fully. If it contains images, note the image paths and read key ones separately.

**Step 2 — Discuss.**
Surface 3-5 key takeaways and ask Dennis: "Anything here you want to emphasize or de-emphasize before I file it?"

**Step 3 — Write the source page.**
Create `wiki/sources/<slug>.md` using the source page format. Slug = kebab-case of the title.

**Step 4 — Update entity and concept pages.**
For every platform, tool, pattern, or framework mentioned significantly in the source:
- If the page exists: update it. Add new information, note contradictions, update `sources` count and `last_updated`.
- If the page doesn't exist: create it using the appropriate template.

**Step 5 — Update overview.md.**
If the source shifts the overall picture — adds a new consideration, challenges a previous claim, introduces a new concept — update `wiki/overview.md` accordingly.

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

**Step 2 — Read relevant pages** (source, entity, concept, solution as needed).

**Step 3 — Synthesize and answer.** Lead with the direct answer. Cite pages. Flag uncertainty.

**Step 4 — Offer to file.** If the answer is non-trivial (an architecture comparison, a design decision memo, a client recommendation), offer: "Want me to file this as an analysis page?" If yes, write `wiki/analyses/<slug>.md` and append to log.md.

---

### Lint Workflow

Triggered by Dennis saying "lint the wiki" or periodically suggested after every 10 ingests.

Check for:
- Pages with no inbound links (orphans)
- Entity pages with `[unknown]` fields that newer sources could fill
- Contradictions between pages that haven't been resolved
- Concepts mentioned in source pages but lacking their own concept page
- Solution pages referencing entities/concepts that don't exist yet
- Claims in overview.md superseded by newer sources
- Missing cross-references

Output: a lint report in chat. Offer to file it as `wiki/analyses/lint-YYYY-MM-DD.md` if useful.

---

## Index Conventions

`index.md` is organized into five sections: Solutions, Sources, Entities, Concepts, Analyses.

Each entry: `| [[slug]] | One-line description | YYYY-MM-DD |`

Solutions section leads because it's Dennis's IP — the primary differentiator of this wiki.

The index is the LLM's navigation tool — keep descriptions specific enough to be useful at a glance.

---

## Log Conventions

`log.md` is append-only. Never edit or delete past entries.

Entry header format: `## [YYYY-MM-DD] <type> | <Title>`
Types: `ingest`, `query`, `lint`, `analysis`

Each entry includes: what happened, what changed, one-line synthesis note.

Grep-friendly: `grep "^## \[" Memory/research/salesforce-architect/log.md` returns all entries in order.

---

## Cross-Referencing Rules

- Use Obsidian wikilinks: `[[slug]]` for pages within this wiki.
- Always link entity and concept names on first mention in a page — don't repeat links within the same page.
- Solution pages link to the entities/concepts they implement. Entity/concept pages list solutions that use them. Source pages link to the entities/concepts they update.
- This bidirectional linking is what makes the wiki navigable.

---

## Overview.md Conventions

`wiki/overview.md` is the master synthesis — the evolving answer to: *"What do I know about Salesforce architecture, and where does my own practice stand?"*

It is not an index. It is a living memo. It should:
- Lead with the current thesis (2-3 sentences on Dennis's architectural perspective and practice)
- Organize key insight clusters by domain (integration, data, devops, etc.)
- Surface Dennis's most reusable patterns from solutions/
- Flag open questions, gaps in knowledge, and areas to deepen
- Note where external knowledge is thin or contradictory

Update it on every ingest that meaningfully shifts the picture.

---

## Naming Conventions

- Slugs: `kebab-case`, lowercase, no special characters
- Entity slugs: product/tool name (`sales-cloud`, `mulesoft`, `copado`, `data-cloud`)
- Concept slugs: pattern name (`platform-events`, `large-data-volumes`, `metadata-api`, `change-data-capture`)
- Solution slugs: descriptive context (`cpq-migration-financial-services-2024`, `service-cloud-ctia-omnichannel`)
- Source slugs: abbreviated title (`docs-platform-events-overview`, `yt-andy-mulesoft-patterns-2025`)
- Analysis slugs: descriptive + date (`integration-pattern-comparison-2026-04`)

---

## Session Start Protocol

At the start of any session touching this wiki:
1. Read `CLAUDE.md` (this file)
2. Read `index.md` to understand current wiki state
3. Read the last 3 entries in `log.md` for recent context
4. Read `wiki/overview.md` for current thesis

Then proceed with the session task.
