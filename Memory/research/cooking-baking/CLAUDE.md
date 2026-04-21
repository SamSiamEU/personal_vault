# Cooking & Baking Wiki — Operating Manual

> Read this at the start of every session touching this wiki. Defines structure, conventions, and workflows.

---

## Purpose

A compounding knowledge base on **cooking, baking, and culinary knowledge** — techniques, recipes, ingredient science, and kitchen craft. Personal passion project, not professional work.

**Scope:**
- Recipes (tested and reference — clearly marked)
- Cooking techniques (sautéing, braising, emulsification, Maillard reaction, etc.)
- Baking science (gluten development, fermentation, fat ratios, leavening agents)
- Ingredient knowledge (varieties, substitutions, flavor profiles, sourcing)
- Cuisines and culinary traditions
- Equipment and tools
- Key sources: Kenji López-Alt, Samin Nosrat, Claire Saffitz, Serious Eats, NYT Cooking, Modernist Cuisine

**Out of scope:**
- Nutrition/diet tracking
- Restaurant reviews (unless they yield a technique or recipe worth capturing)

---

## Directory Structure

```
Memory/research/cooking-baking/
├── CLAUDE.md          ← This file. Read first, every session.
├── index.md           ← Content catalog. Updated on every ingest.
├── log.md             ← Append-only activity log. Never delete entries.
├── raw/               ← Source documents. IMMUTABLE — read only, never edit.
│   └── assets/        ← Downloaded images, recipe scans.
└── wiki/
    ├── overview.md    ← Evolving synthesis. Updated when the picture shifts.
    ├── entities/      ← One page per ingredient, cuisine, equipment type, or chef.
    ├── concepts/      ← One page per technique, method, or culinary principle.
    ├── sources/       ← One page per ingested source (cookbook, article, video).
    └── analyses/      ← Filed comparisons, recipe variations, technique breakdowns.
```

**Hard rule:** `raw/` is append-only. Never modify, rename, or delete raw sources.

---

## Page Formats

### Entity Page (`wiki/entities/<slug>.md`)

Used for: ingredients, cuisines, equipment, chefs/authors.

```markdown
---
name: <Ingredient / Cuisine / Equipment / Person>
type: entity
category: <ingredient | cuisine | equipment | chef-author>
tags: [<tag1>, <tag2>]
sources: <count>
last_updated: YYYY-MM-DD
---

# <Name>

## What It Is
One paragraph. What it is, where it comes from, key characteristics.

## How to Use
Key applications, pairings, or techniques. When it shines.

## Varieties / Types
Notable variations worth distinguishing (e.g., for flour: bread, AP, cake, 00).

## Storage & Sourcing
How to store it, what to look for when buying, substitutions.

## Gotchas
Common mistakes, pitfalls, or things that surprise first-timers.

## Sources
- [[source-slug]] — one-line note
```

### Concept Page (`wiki/concepts/<slug>.md`)

Used for: techniques, methods, and culinary principles.

```markdown
---
name: <Technique / Concept Name>
type: concept
category: <technique | baking-science | flavor | heat-method | fermentation>
tags: [<tag1>, <tag2>]
sources: <count>
last_updated: YYYY-MM-DD
---

# <Concept Name>

## Definition
What this technique or principle is.

## How It Works
The science or mechanism behind it. Why it matters.

## How to Do It
Step-by-step or key parameters (temperature, time, ratios).

## Common Mistakes
- What goes wrong and why.

## Sources
- [[source-slug]] — one-line note
```

### Source Page (`wiki/sources/<slug>.md`)

```markdown
---
title: <Original Title>
type: source
format: <cookbook | article | youtube | podcast | recipe>
url: <original URL or file path>
author: <author or channel>
date_published: YYYY-MM-DD
date_ingested: YYYY-MM-DD
tags: [<tag1>, <tag2>]
---

# <Title>

## Summary
3-5 sentences. Core content and why it's worth keeping.

## Key Takeaways
- Bullet list of techniques, ratios, tips, or recipes captured.

## Notable Recipes / Techniques
List specific recipes or techniques extracted, with brief notes.

## Wiki Pages Updated
- [[slug]] — what was added/changed

## Gaps / Follow-up
- What to try or explore next.
```

### Analysis Page (`wiki/analyses/<slug>.md`)

Used for: recipe comparisons, technique experiments, variation breakdowns.

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
## Verdict / What to Try Next
```

---

## Workflows

### Ingest Workflow

Triggered when Dennis drops a source into `raw/` or pastes a recipe/article and says "ingest."

1. Read the source fully.
2. Surface 3-5 key takeaways or techniques. Ask: "Anything to emphasize before I file it?"
3. Write `wiki/sources/<slug>.md`.
4. Update or create entity and concept pages as needed.
5. Update `wiki/overview.md` if the ingest meaningfully adds to the picture.
6. Update `index.md`.
7. Append to `log.md`: `## [YYYY-MM-DD] ingest | <Title>`

### Query Workflow

1. Read `index.md` to find relevant pages.
2. Read relevant pages.
3. Synthesize and answer. Cite pages. Flag if advice is source-dependent (e.g., Kenji vs. Samin differ).
4. Offer to file as an analysis page for recipe comparisons or technique experiments.

### Lint Workflow

Triggered by "lint the wiki." Check for orphans, missing technique pages for referenced methods, stale overview. Report in chat.

---

## Conventions

- **Slugs:** `kebab-case`, lowercase. Entity: `sourdough-starter`, `cast-iron`, `kenji-lopez-alt`. Concept: `maillard-reaction`, `autolyse`, `dry-brine`. Source: `book-food-lab`, `yt-claire-croissants-2023`.
- **Links:** Obsidian wikilinks `[[slug]]`. Link on first mention per page only.
- **Index:** Four sections — Sources, Entities, Concepts, Analyses. Each entry: `| [[slug]] | One-line description | YYYY-MM-DD |`
- **Log:** Append-only. Format: `## [YYYY-MM-DD] <type> | <Title>`. Types: `ingest`, `query`, `lint`, `analysis`.

---

## Session Start Protocol

1. Read `CLAUDE.md` (this file)
2. Read `index.md`
3. Read last 3 entries in `log.md`
4. Read `wiki/overview.md`
