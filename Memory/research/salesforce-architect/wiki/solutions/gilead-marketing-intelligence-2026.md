---
name: Gilead Marketing Intelligence — DTC Pharma Analytics
type: solution
category: presentation
client: Gilead Sciences
date: 2026-02-27
tags: [marketing-intelligence, data-cloud, mta, hva, pharma, dtc, tableau-next, agentforce, paid-media, sdm]
status: active
---

# Gilead Marketing Intelligence — DTC Pharma Analytics

## Context

Gilead's data and measurement teams were operating with fragmented analytics: separate reporting for addressable, social, and programmatic ads with no unified view. Campaign result reporting took 8–10 weeks. The team needed:

1. A single source of truth replacing fragmented analytics tools
2. Multi-Touch Attribution (MTA) to prove the correlation between digital engagement and tangible business outcomes (Rx claim increases, PSP enrollments)
3. Proprietary audience and segment creation using internal data sets
4. Measurement capability that ingests campaign data from all channels into Data Cloud
5. Orchestration and automated campaign optimization based on real-time insights
6. Movement from reactive reporting to proactive recommendations

Salesforce proposed **Marketing Intelligence** built on Data Cloud and Tableau Next as the unified analytics and measurement layer.

## Decision / Approach

Marketing Intelligence was proposed as a three-capability stack:

1. **Prove ROI with MTA** — multi-touch attribution tracking every patient touchpoint from unbranded search to PSP enrollment, proving value of awareness and nurture channels beyond last-click
2. **From Volume to Value (HVAs)** — moving beyond impression metrics to patient intent signals configured as High-Value Actions
3. **Connect & Harmonize Marketing Data** — MI's semantic data model (SDM) as the unified data pipeline, ingesting all paid/owned channel data into Data Cloud

Target state: campaign result reporting compressed from 8–10 weeks → 3–4 weeks.

## Rationale

Gilead's DTC pharma model maps naturally to MI's architecture:
- Patient journey has clear funnel stages (Awareness → Consideration/Decision → Conversion) that map directly to HVA configuration
- Rx claims and PSP enrollments are high-latency conversion events — MTA is the only attribution model that can connect early-funnel digital engagement to these outcomes; last-click fails entirely in this context
- Data is siloed across Meta, Google, programmatic, email, and web — MI's SDM is designed for exactly this harmonization problem
- The 8–10 week reporting lag suggests manual ETL and spreadsheet workflows; MI's OOTB connectors and pre-built data model eliminate that work
- Agentforce autonomous optimization closes the loop from insight to budget adjustment without waiting for analyst review cycles

## Key Components

### Data Pipeline Architecture

MI's data pipeline has two ingestion paths depending on whether the source has an OOTB connector:

**Path 1 — Managed OOTB API Connector (standard paid media sources)**
```
Paid Media Source (Meta, Google, programmatic)
  ↓ [OOTB API Connector — no implementation partner needed]
Data Ingestion
  ↓
Data Stream → Raw DLOs
  ↓ [Transform: Add IDs + Enrichments]
Ads DLO (with Ads Formulas)
  ↓
Delivery Report Data Stream → Delivery Report DLO → Star Schema
Conv. Report Data Stream  → Conv. DLO           → Star Schema
  ↓
SDM (Locked):
  Campaign DMO
  AdGroup DMO
  Creative DMO
  Ads Facts DMO
  Segment DMO
  → Calc Dims + Calc Meas
  ↓
MI Dashboards (Data Cloud Reports + Tableau Next)
```

**Path 2 — Total Connect (custom API, non-standard sources)**
```
Custom/Non-standard Source
  ↓ [Total Connect — Custom API connector]
Data Ingestion
  ↓
Data Stream → Raw DLOs
  ↓ [Transform: Add IDs + Enrichments + Manual Mapping]
Star Schema → DMO1, DMO2, DMO3, Campaign DMO
  ↓
SDM (Locked) — inherits locked objects from managed SDM
  ↓
Custom (Open) SDM:
  + New Relationships
  + New Calc Dims
  + New Calc Meas
  ↓
MI Dashboards (Data Cloud Reports + Tableau Next)
```

The locked SDM ensures schema consistency across all connectors; the open SDM layer allows Gilead-specific extensions (custom metrics, pharma KPIs like Cost Per Enrollment) without breaking the base model.

### Semantic Data Model (SDM) Objects

Pre-built objects auto-populated when connectors are configured:
- **Campaign DMO** — campaign-level metadata and performance
- **AdGroup DMO** — ad group hierarchy within campaigns
- **Creative DMO** — individual creative assets (copy, imagery)
- **Ads Facts DMO** — impression/click/conversion event facts
- **Segment DMO** — audience segment definitions and performance

Pre-built metrics: CPC, CTR, Cost Per Enrollment (configurable), ROAS.

Pre-built relationships: which Ads belong to which Campaigns, which CreativeS map to which AdGroups.

### High-Value Actions (HVAs) — Pharma DTC Funnel

Configured to track patient intent signals across the full DTC funnel:

| Stage | HVA Events |
|-------|-----------|
| **Awareness** | Symptom Checker Tool interaction, Prevention Guide Download, Daily Pill vs Injection Article read |
| **Consideration & Decision** | Find a Doctor tool use, Doctor Discussion Guide download, "How it Works" Video view |
| **Conversion** | QR Code Scan (doctor's office), Treatment Adherence Program Sign-Up, PSP Enrollment |

HVAs replace impression/click-based KPIs with patient-intent signals. This allows campaign optimization toward actual patient progress rather than vanity metrics.

### Multi-Touch Attribution (MTA)

Tracks every patient touchpoint from unbranded search through PSP enrollment. Attributes credit across:
- **Initiator channels** — channels that start the patient journey (typically unbranded search, social awareness)
- **Nurture channels** — channels that move patients from awareness to consideration
- **Conversion channels** — channels that close PSP enrollment

Enables proving value of awareness and nurture campaigns that traditional last-click attribution would zero out.

### Cross-Channel Segment Intelligence

Unified Tableau Next dashboard showing paid (Meta, Google) and owned (Email, SMS) channel performance for the same audience segment side-by-side. Enables:
- Identifying segments with high cost but low ROAS on one channel
- Drilling down to demographic performance within segments
- Budget reallocation decisions based on cross-channel ROAS (e.g., move Meta budget to Google Search for a specific segment)

### Agentforce Autonomous Optimization

Agentforce agents integrated with MI can make real-time budget adjustments based on MI insights — adjusting live campaigns, pausing underperformers, scaling high-ROAS ad groups without requiring analyst intervention or waiting for weekly reporting cycles.

## Reusability

This pattern applies to any pharma DTC client with:
- Multi-channel digital campaigns across paid search, social, programmatic
- High-latency conversion events (PSP enrollment, Rx fill, program sign-up) that don't map to last-click attribution
- Patient/HCP journey analytics with distinct funnel stages
- Fragmented analytics tools that need consolidating

The HVA funnel template (Awareness → Consideration/Decision → Conversion) is reusable across pharma brands — only the specific event names change per drug/program.

For non-pharma clients: the same pattern applies wherever conversion events are high-latency and multi-touch (B2B sales, financial services, healthcare enrollment). The SDM objects are agnostic — Campaign/AdGroup/Creative/Touchpoint apply universally.

**Total Connect path** is the integration pattern when a Gilead-specific data source (internal data warehouse, proprietary attribution vendor, or niche ad platform) doesn't have an OOTB MI connector. The locked + open SDM model means custom extensions don't break the standard MI schema — document this distinction for clients who immediately ask "what about our [X] data that isn't in the connector library."

## Lessons Learned

- The 8–10 week reporting lag is a strong anchor for business value — quantifying the improvement (to 3–4 weeks) resonates immediately with data teams and creates a concrete before/after story
- Lead with HVAs, not MTA — HVAs are tangible and visual (patient journey stages), MTA is conceptual; get alignment on what counts as a meaningful action first, then show how MTA attributes credit across those actions
- The locked SDM is a selling point, not a constraint — it means "no manual data modeling and no waiting on data teams"; frame the open layer as extensibility for pharma-specific KPIs
- Agentforce autonomous optimization is a conversation-starter but requires guardrail discussion — autonomous budget changes on high-spend pharma campaigns need defined approval thresholds; raise this proactively rather than letting it surface as an objection

## Related Pages

- [[marketing-intelligence]] — MI product entity (capabilities, architecture, SDM objects)
- [[data-360]] — Data Cloud as the underlying data foundation for MI pipelines
- [[agentic-design-patterns]] — Agentforce autonomous optimization pattern
- [[cross-cloud-data-models]] — cross-cloud data architecture context for pharma
