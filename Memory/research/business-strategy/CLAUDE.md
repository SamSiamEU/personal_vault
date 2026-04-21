# Business Strategy Wiki — Operating Manual

> Read this at the start of every session touching this wiki. Defines structure, conventions, and workflows.

---

## Purpose

A compounding knowledge base on **business frameworks, leadership, scaling, and strategic thinking**. Pure learning and reference — used to challenge and sharpen Dennis's own thinking, not to document client work.

**Scope:**
- Business strategy frameworks (Porter, Blue Ocean, Jobs to Be Done, Wardley Maps, etc.)
- Company building and scaling (0→1, product-market fit, org design, hiring, culture)
- Leadership and management (decision-making, communication, feedback, team dynamics)
- Finance and unit economics (SaaS metrics, P&L literacy, fundraising, valuation)
- Go-to-market strategy (positioning, pricing, distribution, category creation)
- Mental models and thinking frameworks (first principles, inversion, second-order effects)
- Key thinkers: Ben Horowitz, Patrick Lencioni, Hamilton Helmer, Hamilton Wright, etc.
- Books, podcasts, essays that challenge assumptions

**Out of scope:**
- Salesforce-specific GTM (covered in salesforce-architect wiki)
- Acqura product strategy (covered in acqura-intel wiki)
- Operational how-tos for Dennis's specific businesses

---

## Directory Structure

```
Memory/research/business-strategy/
├── CLAUDE.md          ← This file. Read first, every session.
├── index.md           ← Content catalog. Updated on every ingest.
├── log.md             ← Append-only activity log. Never delete entries.
├── raw/               ← Source documents. IMMUTABLE — read only, never edit.
│   └── assets/        ← Downloaded images, diagrams.
└── wiki/
    ├── overview.md    ← Evolving synthesis. Updated when the picture shifts.
    ├── entities/      ← One page per company, person, or firm.
    ├── concepts/      ← One page per framework, mental model, or business term.
    ├── sources/       ← One page per ingested source.
    └── analyses/      ← Filed query outputs and comparisons.
```

**Hard rule:** `raw/` is append-only. Never modify, rename, or delete raw sources.

---

## Page Formats

### Entity Page (`wiki/entities/<slug>.md`)

```markdown
---
name: <Company / Person Name>
type: entity
category: <company | person | firm | book-author>
tags: [<tag1>, <tag2>]
sources: <count>
last_updated: YYYY-MM-DD
---

# <Name>

## Who / What They Are
One paragraph. Role, background, why they matter.

## Core Contribution
The idea, framework, or example they're known for in this wiki.

## Key Lessons
- Bullet list.

## Contradictions / Nuance
- Where this person/company's story is more complex than the headline.

## Sources
- [[source-slug]] — one-line note
```

### Concept Page (`wiki/concepts/<slug>.md`)

```markdown
---
name: <Concept / Framework Name>
type: concept
category: <strategy | leadership | scaling | finance | gtm | mental-model>
tags: [<tag1>, <tag2>]
sources: <count>
last_updated: YYYY-MM-DD
---

# <Concept Name>

## Definition
Clear, concise definition or description of the framework.

## How It Works
Mechanism, steps, or mental model.

## When to Use
The scenarios where this applies. What question it answers.

## Limitations / Failure Modes
Where the framework breaks down or misleads.

## Dennis's Take
How this concept applies to Dennis's actual context — Acqura, Sam Siam, Eksido, or general practice.

## Sources
- [[source-slug]] — one-line note
```

### Source Page (`wiki/sources/<slug>.md`)

```markdown
---
title: <Original Title>
type: source
format: <book | article | podcast | youtube | essay | thread>
url: <original URL or file path>
author: <author or channel>
date_published: YYYY-MM-DD
date_ingested: YYYY-MM-DD
tags: [<tag1>, <tag2>]
---

# <Title>

## Summary
3-5 sentences. Core argument or content.

## Key Takeaways
- Bullet list.

## Notable Quotes
> "Direct quote if striking."

## Wiki Pages Updated
- [[slug]] — what was added/changed

## Gaps / Follow-up
- What to explore next.
```

### Analysis Page (`wiki/analyses/<slug>.md`)

```markdown
---
title: <Analysis Title>
type: analysis
question: <The question this answers>
date: YYYY-MM-DD
tags: [<tag1>, <tag2>]
---

# <Title>

## Question
## Answer
## Supporting Evidence
## Limitations
```

---

## Workflows

### Ingest Workflow

Triggered when Dennis drops a source into `raw/` or pastes content and says "ingest."

1. Read the source fully.
2. Surface 3-5 key takeaways. Ask: "Anything to emphasize before I file it?"
3. Write `wiki/sources/<slug>.md`.
4. Update or create entity and concept pages as needed.
5. Update `wiki/overview.md` if the ingest shifts the picture.
6. Update `index.md`.
7. Append to `log.md`: `## [YYYY-MM-DD] ingest | <Title>`

### Query Workflow

1. Read `index.md` to find relevant pages.
2. Read relevant pages.
3. Synthesize and answer. Cite pages. Flag uncertainty.
4. Offer to file as an analysis page if the answer is non-trivial.

### Lint Workflow

Triggered by "lint the wiki." Check for orphans, unfilled fields, missing concept pages, stale overview claims. Report in chat; offer to file as `wiki/analyses/lint-YYYY-MM-DD.md`.

---

## Conventions

- **Slugs:** `kebab-case`, lowercase. Entity: `ben-horowitz`, `stripe`. Concept: `jobs-to-be-done`, `7-powers`, `first-principles`. Source: `book-hard-thing-about-hard-things`, `pod-acquired-stripe-2024`.
- **Links:** Obsidian wikilinks `[[slug]]`. Link on first mention per page only.
- **Index:** Four sections — Sources, Entities, Concepts, Analyses. Each entry: `| [[slug]] | One-line description | YYYY-MM-DD |`
- **Log:** Append-only. Format: `## [YYYY-MM-DD] <type> | <Title>`. Types: `ingest`, `query`, `lint`, `analysis`.

---

## Session Start Protocol

1. Read `CLAUDE.md` (this file)
2. Read `index.md`
3. Read last 3 entries in `log.md`
4. Read `wiki/overview.md`
