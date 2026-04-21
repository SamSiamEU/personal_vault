---
name: Marketing Intelligence (Salesforce)
type: entity
category: salesforce-cloud
tags: [marketing-intelligence, paid-media, analytics, mta, tableau, data-360, agentforce]
sources: 1
last_updated: 2026-04-21
---

# Marketing Intelligence (Salesforce)

## What It Is
Salesforce Marketing Intelligence is a paid-media analytics and optimization platform built on Salesforce Platform, Data Cloud, and Tableau Next. It provides a connector library for paid media channels, a pre-built Semantic Data Model (SDM), multi-touch attribution (MTA), and Agentforce-powered autonomous campaign optimization. Positioned for marketing analytics and measurement teams who need to unify paid and owned channel performance data and prove ROI.

Distinct from Marketing Cloud (email/journey automation): Marketing Intelligence is an analytics/intelligence layer, not a campaign execution platform.

## Relevance to Architecture Work
- When clients want to unify paid media performance (Meta, Google, programmatic) with owned channel data (email, SMS, CRM) under one analytics view
- When MTA is required — proving attribution across the full funnel (awareness → conversion/Rx enrollment/etc.)
- When the client wants to replace fragmented reporting tools (GA4 + Meta Ads Manager + Looker etc.) with a single source of truth on the Salesforce Platform
- When autonomous AI-driven campaign optimization is a requirement — Agentforce agents adjust live campaigns without human intervention

## Key Capabilities
- **Pre-built connector library**: 3-click connection to major paid media platforms (Meta, Google Ads, programmatic); no partner required for standard connections
- **Semantic Data Model (SDM)**: pre-built objects (Campaign, Ad, AdGroup, Creative, Segment, Touchpoint), relationships (which Ads belong to which Campaigns), and metrics (CPC, CTR, Cost Per Enrollment) — automatically populated when connectors are configured; OOTB Tableau Next visualizations
- **Multi-Touch Attribution (MTA)**: tracks every customer touchpoint from awareness through conversion; attributes credit across channels; surfaces which channels initiate, nurture, and close
- **High-Value Actions (HVAs)**: configure custom conversion events (not just clicks/impressions) — for pharma: symptom checker visit → doctor discussion guide → PSP enrollment; for retail: add-to-cart → purchase
- **Cross-Channel Segment Intelligence**: unified Tableau Next dashboard showing audience performance across paid (Meta, Google) and owned (Email, SMS) channels simultaneously; supports budget reallocation decisions
- **Agentforce integration**: autonomous agents that make real-time budget adjustments and campaign optimizations based on MI insights; "activate autonomous insights" without human intervention
- **Tableau Next as visualization layer**: all MI dashboards built on Tableau Next; shared data models reusable across the entire business
- **Data Cloud foundation**: MI data pipelines write to Data Cloud DMOs + DLOs via SDM; zero-copy between MI and other Data Cloud use cases (segmentation, identity resolution, Agentforce grounding)

## Architecture
```
Paid Media Sources (Meta, Google, programmatic, email, SMS)
    ↓  [API Connectors — 3-click, OOTB]
Data Ingestion Layer (Data Cloud Data Streams + DLOs)
    ↓  [SDM Transformation]
Semantic Data Model (Campaign/Ad/AdGroup/Creative/Segment DMOs + Calculated Insights)
    ↓  [Tableau Next + Data Cloud Reports]
MI Dashboards (DCR) — embedded in Salesforce
    ↓  [Agentforce Actions]
Autonomous Campaign Optimization (budget adjustments, pause/scale)
```

## Licensing / Pricing
- [Specific rates unknown] — built on Salesforce Platform; requires Data Cloud licensing
- Standard paid media connectors appear to be included; "Total Connect" (custom API) may be separate
- Consumption-based Data Cloud credits apply to data processing

## Strengths
- "Connect in 3 clicks" for major paid media sources — fast time to value vs. custom ETL
- Pre-built SDM means no manual data modeling for marketing analytics use cases
- Unified view of paid + owned (email, SMS) channel performance — rare capability
- Agentforce autonomous optimization closes the loop from insight to action
- Native Data Cloud integration means MI data can be reused for segmentation, agents, clean rooms

## Weaknesses / Gaps
- Connector library may not cover all niche/regional ad platforms — validate coverage before committing
- Autonomous campaign optimization via Agentforce is new — maturity and guardrails need evaluation for high-spend campaigns
- "Total Connect" (custom API connector) mentioned for non-standard sources — complexity unknown
- Performance for very large accounts (high-frequency ad data, 10M+ events/day) not documented

## Known Gotchas
- MI is NOT Marketing Cloud (email automation) — these are two separate products that serve different functions; architects must clearly distinguish them in client conversations
- Tableau Next is the required visualization layer — clients already using Looker/Power BI/Tableau Classic will face a migration/parallel tool discussion
- Agentforce autonomous optimization requires careful guardrail design — uncontrolled autonomous budget changes can be costly

## Contradictions / Open Questions
- How does Marketing Intelligence relate to the Marketing Cloud Analytics (CRM Analytics) dashboards already in use?
- Is the SDM a superset of Data Cloud's standard marketing DMOs, or a specialized schema on top?
- What is the licensing relationship between Marketing Intelligence and Marketing Cloud Growth/Advanced Edition?

## Sources
- Gilead Presentation MI 2_26_26 PDF (own IP — presales deck) — product overview, SDM architecture diagram, MTA + HVAs use cases, pharma DTC application, Agentforce integration
