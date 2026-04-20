---
date: 2026-04-20
source: youtube
url: 
author/channel: Herk (YouTube)
stream: ai-claude
tags: [obsidian, claude-code, llm-wiki, knowledge-management, rag, karpathy]
notebooklm: false
---

# LLM Wiki — Build a Personal Knowledge System in 5 Minutes

## In One Sentence
Use Claude Code + Obsidian to automatically ingest raw content into an interconnected markdown wiki that compounds knowledge over time.

## Key Insights

- Knowledge compounds like interest — unlike normal AI chats where knowledge disappears, an LLM wiki persists and grows
- No fancy infrastructure needed — just markdown files. No vector database, no embeddings
- Two folder structure — raw/ (dump content here) and wiki/ (Claude organizes it automatically)
- Hot cache — a 500-word summary of most recent context, useful for executive assistant use cases
- Linting — periodic health checks where Claude finds inconsistencies and suggests new articles
- LLM Wiki vs RAG — wiki wins at small-medium scale, traditional RAG wins at millions of documents

## How This Connects To My Work

- Acqura: Simpler markdown-first approach worth considering before jumping to Postgres + pgvector
- Personal vault: My research/ folder already mirrors this pattern
- Eksido: Could build a client knowledge wiki from briefs and meeting notes

## Open Questions This Raised

- Should I implement simple markdown wiki for Phase 3 before building Postgres + pgvector?
- Could I use Obsidian Web Clipper to feed acqura-intel/ automatically?

## Actions / Next Steps

- Install Obsidian Web Clipper Chrome extension
- Try Karpathy LLM wiki prompt in Claude Code on personal_vault
- Reconsider Phase 3 — start with markdown wiki, graduate to pgvector only if scale demands it

## Techniques / Prompts To Try

Karpathy setup prompt — paste into Claude Code inside your vault:
You are now my LLM wiki agent. Implement this exact idea as my complete second brain. Guide me step by step. Create the CLAUDE.md schema.

Then drop content into raw/ and say:
Ingest the new file in raw/ into the wiki
