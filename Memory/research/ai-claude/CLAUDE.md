# AI & Claude Wiki — Operating Manual

> Read this at the start of every session touching this wiki. Defines structure, conventions, and workflows.

---

## Purpose

A compounding knowledge base on **AI tools, Claude capabilities, prompting techniques, and agentic workflows**. Pure learning and reference — no own IP, no client deliverables.

**Scope:**
- Claude features, models, and API (Claude Code, Projects, artifacts, tool use, caching, thinking)
- Prompting techniques (chain-of-thought, few-shot, system prompts, prompt engineering patterns)
- Agentic workflows (multi-agent systems, memory architectures, orchestration patterns)
- AI coding tools (Claude Code, Cursor, Copilot, Windsurf, etc.)
- LLM concepts (context windows, embeddings, RAG, fine-tuning, evals)
- Other frontier AI tools and models (GPT-4o, Gemini, Mistral, open source)
- Community resources: Andrej Karpathy, Simon Willison, Ethan Mollick, Anthropic blog, AI Twitter

**Out of scope:**
- General software engineering not tied to AI workflows
- Salesforce AI features (covered in salesforce-architect wiki)

---

## Directory Structure

```
Memory/research/ai-claude/
├── CLAUDE.md          ← This file. Read first, every session.
├── index.md           ← Content catalog. Updated on every ingest.
├── log.md             ← Append-only activity log. Never delete entries.
├── raw/               ← Source documents. IMMUTABLE — read only, never edit.
│   └── assets/        ← Downloaded images, screenshots.
└── wiki/
    ├── overview.md    ← Evolving synthesis. Updated when the picture shifts.
    ├── entities/      ← One page per tool, model, platform, or person.
    ├── concepts/      ← One page per technique, pattern, or AI term.
    ├── sources/       ← One page per ingested source.
    └── analyses/      ← Filed query outputs and comparisons.
```

**Hard rule:** `raw/` is append-only. Never modify, rename, or delete raw sources.

---

## Page Formats

### Entity Page (`wiki/entities/<slug>.md`)

```markdown
---
name: <Tool / Model / Person Name>
type: entity
category: <model | tool | platform | person | lab>
tags: [<tag1>, <tag2>]
sources: <count>
last_updated: YYYY-MM-DD
---

# <Name>

## What It Is
One paragraph. What it does or who they are.

## Why It Matters
Key relevance — what this changes about how AI is used or understood.

## Key Capabilities / Ideas
- Bullet list.

## Limitations / Gotchas
- ...

## Sources
- [[source-slug]] — one-line note
```

### Concept Page (`wiki/concepts/<slug>.md`)

```markdown
---
name: <Concept Name>
type: concept
category: <prompting | agentic | architecture | model-behavior | tool-use | eval>
tags: [<tag1>, <tag2>]
sources: <count>
last_updated: YYYY-MM-DD
---

# <Concept Name>

## Definition
Clear, concise definition.

## How It Works
Mechanism or mental model.

## When to Use
Practical scenarios.

## Key Constraints / Trade-offs
- ...

## Sources
- [[source-slug]] — one-line note
```

### Source Page (`wiki/sources/<slug>.md`)

```markdown
---
title: <Original Title>
type: source
format: <article | youtube | docs | podcast | thread | paper>
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

## Notable Quotes / Data Points
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

Triggered by "lint the wiki." Check for orphans, unfilled `[unknown]` fields, missing concept pages, stale overview claims. Report in chat; offer to file as `wiki/analyses/lint-YYYY-MM-DD.md`.

---

## Conventions

- **Slugs:** `kebab-case`, lowercase. Entity: `claude-code`, `andrej-karpathy`. Concept: `chain-of-thought`, `rag`, `prompt-caching`. Source: `yt-karpathy-llm-intro-2024`, `docs-claude-tool-use`.
- **Links:** Obsidian wikilinks `[[slug]]`. Link on first mention per page only.
- **Index:** Four sections — Sources, Entities, Concepts, Analyses. Each entry: `| [[slug]] | One-line description | YYYY-MM-DD |`
- **Log:** Append-only. Format: `## [YYYY-MM-DD] <type> | <Title>`. Types: `ingest`, `query`, `lint`, `analysis`.

---

## Session Start Protocol

1. Read `CLAUDE.md` (this file)
2. Read `index.md`
3. Read last 3 entries in `log.md`
4. Read `wiki/overview.md`
