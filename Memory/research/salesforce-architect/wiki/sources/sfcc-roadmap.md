---
title: SFCC Roadmap Items (B2C Commerce Cloud)
type: source
format: pdf
url: raw/SFCC Roadmap items.pdf
author: Salesforce (Commerce Cloud Product)
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [commerce-cloud, sfcc, roadmap, composable-storefront, search, ai, data-360, payments, mcp]
---

# SFCC Roadmap Items (B2C Commerce Cloud)

## Summary
Salesforce B2C Commerce Cloud (SFCC) product roadmap document covering upcoming and recently GA capabilities across payments, search, AI, marketing integration, social commerce, and enterprise trust. Most items are GA Q4 2025 – H1 2026. Key strategic directions: (1) native AI-powered search replacing 3P search tools, (2) Commerce catalogs becoming discoverable by AI shopping platforms (ChatGPT, Perplexity), (3) Zero Copy integration with Data Cloud eliminating data duplication, (4) MCP tooling for Composable Storefront developers.

## Key Takeaways

### Payments
- **BYO Payments**: bring your own payment gateway without added fees or integration work; native Adyen integration coming (GA Q1 2026); centralized payment management + native checkout components
- Positioned as lower TCO vs. current approach of paying separate gateway fees

### Connected Commerce & Marketing (Data 360 Integration)
- **Zero Copy Access** (GA Q255D — likely GA Q2-Q3 2026): query Commerce Cloud data directly within Data Cloud without copying/storing it in Data Cloud — aligns with Data 360's zero-copy inbound pattern; reduces data storage costs
- **Unified Consent** (SAQ#25m): common consent model across Commerce and Marketing channels; captures consent in Commerce and respects it across all channels — fills the Winter '22 gap where consent management was fragmented
- **Commerce & Marketing Journeys** (GAGT26qD): two-way interactive messaging for commerce flows (WhatsApp, SMS, email); OOTB templates for: welcome new users, abandoned cart, back in stock, price drop, promotion alerts — replaces/supersedes the Winter '22 manual setup pattern
- **Salesforce Personalization Integration**: product recommendations using Data Cloud data (cross-cloud aware)

### B2C Search Evolution (Major Architectural Shift)
Current state: keyword matching + manual synonym dictionaries + basic typo tolerance.

**Incoming capabilities**:

| Feature | Status | What It Does |
|---------|--------|-------------|
| Contextual Search: Semantic Understanding | Pilot Q3/25, GA Q2 2026 | Natural language + intent understanding ("dress for a gala" → formal gowns) |
| Contextual Search: Shopper Context | Beta Q4/25, GA Q2 2026 | Location + session context applied ("beach wedding" + shopper in Miami → lightweight options in shopper's size) |
| Boost & Bury | ETA Q2 2026 | Merchandiser control to promote/demote products in search and category results by segment |
| Native Intelligent Search | Road | Eliminates 3P search tools (Algolia, Coveo, etc.); semantic + context-aware; supported across onsite search and guided shopping agent |

**Strategic implication**: 3P search tools (Algolia, Coveo, Lucidworks) are directly in the crosshairs. For new Commerce implementations, defer 3P search investment pending GA of Native Intelligent Search.

### Composable Storefront Completeness
- Merchandising parity: BOPIS/Ship-from-Store, Multi-ship, Standard/Bonus Products, Google Address Autocomplete (GA Q1 2026)
- Performance: up to 30% lower LCP, 60% lower TBT via deferred scripts, responsive images, partial hydration
- **MCP developer tools (preview)**: Composable Storefront joining the MCP ecosystem — developers can build agents/tools against Commerce storefront via Model Context Protocol
- OMS + Salesforce Payments OOTB integrations (GA Q1 2026)

### Product Discovery in AI Shopping Platforms
- **Catalog indexing for 3P AI platforms** (ChatGPT, Perplexity, etc.) — Q4 2025 / Q1 2026
- Shoppers asking AI assistants for product recommendations see SFCC catalog items
- **In-Line Checkout**: complete purchase directly within AI platform or click-through to storefront
- **AI Analytics**: track traffic, GMV, and conversions from each AI source (OOTB)
- Architecture implication: Commerce Cloud catalogs become RAG-accessible knowledge sources for AI agents

### Social Commerce
- **Meta (Instagram/Facebook)**: FBP/FBC server-side cookies for improved ad attribution; Meta Permalinks (add-to-cart on Meta, checkout on SFCC storefront); streamlined Business Manager setup
- **TikTok Shop**: native integration from Business Manager; Gift with Purchase support; catalog sync (GA Q1 2026)

### Visual Experience Editor
- Page Designer evolving into a unified content/commerce/personalization visual editor
- **Native Content Foundations**: API-first, frontend-agnostic, "agentic ready" — single content source of truth
- **Dynamic & Personalized Experiences** (GA H1 2026): no-code personalization based on business rules or AI
- **Turnkey Home & Content Pages** (GA H1 2026): OOTB pages for Composable Storefront — zero developer setup

### Enterprise Trust & Scale
- **PCI 4.0 support**: eCDN PCI tools, custom rules, Business Manager UI for compliance (GA Nov 2025)
- **Unified Shield — eCDN Threat Protection** (GA Nov 2025): DDoS, bot management, dynamic caching, Log Center visualization
- **Bot Management for DIS**: protects Dynamic Imaging Service from bots bypassing eCDN

## Notable Quotes / Data Points
- "Eliminating the need for costly, complex third-party tools" — explicit 3P search displacement narrative
- MCP developer tools in preview — Commerce Cloud entering agentic ecosystem
- Product Discovery in AI Platforms: Commerce catalogs indexed for ChatGPT et al. — agentic commerce is here
- Zero Copy Access: Commerce → Data Cloud without duplication — strategic Data 360 integration

## Wiki Pages Updated
- [[commerce-cloud]] — Major updates: Zero Copy integration with Data Cloud, Native Intelligent Search, MCP tools for Composable Storefront, AI Shopping Platform discovery, BYO Payments, roadmap timeline
- [[cross-cloud-data-models]] — Zero Copy changes the Commerce → Data Cloud integration pattern; Unified Consent fills Winter '22 gap
- [[data-360]] — Zero Copy Access from Commerce Cloud confirmed as upcoming capability
- [[mcp-a2a-protocols]] — MCP developer tools for Composable Storefront confirms Commerce Cloud as MCP-connected system

## Gaps / Follow-up
- GA dates are estimates from roadmap items — actual GA may shift; verify before committing to client timelines
- "Guided Shopping Agent" mentioned in context of Contextual Search — Agentforce-powered? product name not clear
- Native Content Foundations described as "agentic ready" — what does this mean in practice for agent-authored content?
- B2B Commerce equivalent of these capabilities not covered — this roadmap appears B2C only
