---
name: NEOM CDP Implementation Partner RFP — Merkle Response
type: solution
category: presentation
client: NEOM
date: 2025-02-04
tags: [neom, cdp, data-cloud, multi-org, mulesoft, bigquery, coe, agile-pods, ksa, rfp, composable-cdp, spotify-pod-model, iat, martech-ops]
status: deprecated
---

# NEOM CDP Implementation Partner RFP — Merkle Response

## Context

NEOM — Saudi Arabia's mega-city project — issued an RFP for a CDP Implementation Partner in early 2025. NEOM is not a single entity but a federation of distinct sectors: Sindalah (luxury island resort, B2C), Trojena (mountain ski resort), THE LINE, Oxagon (industrial city), Education, Media, Tonomus (technology), Magna — each with separate business models, audiences, and in some cases separate Salesforce orgs.

The brief called for a CDP partner to implement Salesforce Data Cloud across this multi-sector structure, design a productized architecture that could be consumed across NEOM's data mesh, and establish an ongoing operational delivery model (not just implementation).

Merkle submitted this RFP response dated January 28 / February 4, 2025. Dennis was listed as **Principal Salesforce Data Cloud Leader / VP SF Solution Engineering** on the core team. The bid was lost. NEOM's investment programme has since been curtailed significantly.

The value of this document is not the NEOM outcome — it is the delivery model and architecture framework, which are directly reusable for any large-scale, multi-sector, multi-org CDP implementation.

## Decision / Approach

### Architecture

**1. Multi-org Salesforce (sector-isolated)**
Each NEOM sector runs its own Salesforce org tailored to its business type:
- B2C (Sindalah): Service Cloud + Sales Cloud
- HTD (Health, Tourism, Development): Experience Cloud + Sales Cloud
- Education: Education Cloud + Experience Cloud portals
- CoE: Sales Cloud
- B2B (Media, Oxagon): Experience Cloud + Sales Cloud

**2. Single Marketing Cloud org with sector BUs**
One Marketing Cloud instance; separate Business Units per sector (Trojena, Oxagon, THE LINE, Media, etc.), governed by a top-level BU that centralises asset management, compliance, and training libraries (Trailhead for Companies / myTrailhead for custom onboarding trails).

**3. Dedicated Data Cloud org as centralised hub**
Recommendation: stand up a dedicated Data Cloud org rather than embedding Data Cloud inside each sector org. Simplifies identity resolution, audience segmentation, and governance. When NEOM completes their in-progress multi-org → single-org consolidation project, migrate to that unified org as the Data Cloud home. Data Cloud uses Data Spaces to give each sector isolated identity resolution and segmentation while enabling cross-sector collaboration at the hub level.

**4. BigQuery federated integration (zero-copy native connector)**
BigQuery sits alongside Data Cloud as a processing and pre-staging layer. Key architectural decision: **run identity resolution testing and heavy data transforms in BigQuery before data enters Data Cloud**. Data Cloud is consumption-based — running all identity resolution processes inside Data Cloud is expensive. BigQuery handles the heavy lifting; clean, resolved data is then fed into Data Cloud. This approach was proven at VodafoneZiggo and referenced explicitly in the proposal.

**5. MuleSoft API layer**
MuleSoft as the API gateway for all orchestration and data distribution functions: bi-directional data synchronisation between sector orgs and the Data Cloud hub, standardised API endpoints, REST/ANSI SQL/ODBC/JDBC access for downstream consumers.

**6. CI/CD pipeline for Data Cloud**
Data Cloud metadata and datasets are managed via CI/CD. In Merkle's approach, datasets can be coded precisely enough to be automatically mapped in Data Cloud without manual intervention — the pipeline handles business rules, data transforms, view development, code review, and promotion to PROD.

**7. Data Kits + MC Package Manager**
Core Data Kits standardise data structures across sectors, with sector-specific extensions for unique attributes. Marketing Cloud Package Manager handles journey templates, content blocks, and automation — enabling the CoE to deploy reusable campaign factories across sectors.

**8. Edge computing for physical locations**
For on-site interactions at physical NEOM locations (resorts, visitor centres), edge nodes near each location process event-based triggers with minimal latency. Satellite-based internet access proposed as backup nodes for failover network connectivity.

### Delivery Model — Spotify Agile Pod Model in an IAT Framework

This is the core reusable IP. The model organises the CDP implementation and ongoing operations team into a hierarchical structure of four unit types:

**Squads** (specialised, owns a workstream end-to-end):
- Integration Squad — API development, connector maintenance, data flow optimisation (MuleSoft, native connectors, federated BigQuery)
- Consent & Privacy Squad — GDPR compliance, OneTrust integration, automated consent management across all data ingestion points
- Content Optimisation Squad — dynamic content templates, Einstein Studio AI/ML training, Adobe GenStudio integration

**Tribes** (connect squads to strategic goals, coordinate cross-squad dependencies):
- Integration Tribe — platform interconnectivity; weekly syncs, shared integration health dashboards
- Data Governance & Compliance Tribe — standardised compliance playbooks, regular audits, federated governance toolset
- AI-Driven Marketing Tribe — audience scoring and segmentation strategy, AI/ML content performance

**Chapters** (skill standardisation and knowledge transfer across squads):
- Integration & Security (API) Development Chapter — standardised API frameworks, centrally maintained reusable integration asset repository
- Privacy & Compliance Chapter — unified compliance templates, regulatory training
- AI/ML Optimisation Chapter — shared model performance benchmarks, reusable components for Einstein Studio + Merkle GenCX, agent governance

**Guilds** (cross-tribe innovation and best practice sharing):
- Dynamic Audience Creation Guild — segmentation/audience scoring best practices across tribes
- Content Personalisation Guild — content frameworks across all tribes and regions

This structure enables **parallel execution** across sectors (pods operate independently) while maintaining **centralised governance** (chapters + CoE oversight) and **cross-sector learning** (guilds + tribes).

The CoE also defines a **continuous workstream feedback loop** across three streams: Strategy Stream (value framework, data strategy, stakeholder management), Tech Stream (use case roadmap, regional setup, continuous improvement), Activation Stream (CDP services, personalisation, reporting).

### CDP Use Case Framework (6 Categories)

1. **Data source and types** — ingestion architecture: batch + streaming, ETL for large uploads, OOTB connectors + open API connectors
2. **Data management** — identity schema (multiple identifiers per customer: corporate ID, email, loyalty ID with trust-level metadata), deterministic + probabilistic matching, semantic layer for business-user access, Data Cloud business dictionary, data quality framework (recoding, business rules, re-labelling for AI prompt compatibility)
3. **Unified profiles** — merge/match rules framework with conflict resolution and trust-level prioritisation, B2B + B2C dual-level segmentation (company/household vs. individual), real-time profile updates
4. **Activation, recommendations & analytics** — unified API layer (MuleSoft + Data Cloud), predictive modelling (Einstein Studio, BYOM), NBA/NBO via Marketing Cloud Personalization, predictive analytics in BigQuery visualised via Marketing Cloud Intelligence
5. **Automation and intelligence** — probabilistic matching with confidence scoring, AI-driven segment discovery and automated decisioning (Journey Builder), data science platform (Einstein + open-source Python/R), BYOM for custom propensity models, Agentforce for intelligent services
6. **Security, extensibility, ease of use** — RBAC + Salesforce Shield, 2FA + SSO, OneTrust for consent compliance, open API framework (REST/GraphQL), edge computing infrastructure, Trailhead-based custom training trails + campaign factory self-service tooling

### Marketing Use Case Framework (META → Acquire → Grow → Retain)

- **META** — AI segmentation, audience suppression, attribution transparency; cross-channel integration with unified audience insights
- **Acquire** — micro-segmentation, lookalike modelling, geolocation targeting (Bluetooth mesh network for on-site), lead scoring/qualification, abandon basket recovery, improved first-party match rates, cross-channel attribution, dynamic pricing, real-time event-based personalisation
- **Grow** — NBA/NBO/NBE models, early upsell via incentive optimisation, householding, reinforcement communications, predictive demand modelling, loyalty scoring, AI-driven lifecycle management
- **Retain** — churn/win-back propensity, price sensitivity analysis, sentiment analysis (NLP), data monetisation via partnerships, next-visit prediction, Salesforce Loyalty Management integration

## Rationale

The dedicated Data Cloud org recommendation was driven by NEOM's multi-org reality: embedding Data Cloud in each sector org would fragment identity resolution and make cross-sector audience building impossible. A hub-and-spoke model with Data Cloud at the centre is the correct architecture for any multi-entity organisation that needs a single customer view across its units.

The BigQuery pre-staging decision is a direct cost management strategy — Data Cloud's consumption pricing makes it expensive to use as a transformation engine. Running transforms and identity resolution testing in BigQuery, then feeding clean data to Data Cloud, is the same pattern used at VodafoneZiggo and is now a standard Merkle recommendation for large-scale Data Cloud implementations.

The Spotify Pod Model was chosen because NEOM required both parallel sector delivery (multiple NEOM sectors activating simultaneously) and long-term operational continuity (the CoE needed to outlive the implementation). A traditional waterfall delivery structure would serialise sector rollouts and leave no sustainable operational framework behind.

## Key Components

- Salesforce Data Cloud (dedicated org, Data Spaces per sector)
- Salesforce Marketing Cloud (single org, sector BUs)
- MuleSoft (API gateway, bi-directional sync, REST/ANSI SQL access layer)
- Google BigQuery (federated zero-copy + identity resolution pre-processing layer)
- OneTrust (consent management integration)
- Einstein Studio (predictive modelling, NBA, BYOM)
- Salesforce Agentforce (intelligent services, autonomous decisioning)
- Adobe GenStudio (content production for Content Optimisation Squad)
- Salesforce Loyalty Management (recommended for Retain use cases)
- CI/CD pipeline (automated Data Cloud dataset mapping, PROD promotion)
- Salesforce Trailhead for Companies (sector-specific custom onboarding trails)
- Agile Pod CoE (squads + tribes + chapters + guilds, ongoing delivery + OPS)

## Reusability

**The CoE delivery model is the primary reusable IP from this document.** The Spotify Pod Model inside an IAT framework, with squads/tribes/chapters/guilds mapping to integration, compliance, and AI/ML workstreams, is the correct structure for any of the following:

- Multi-sector or multi-brand CDP rollout (separate sector teams, unified governance)
- Complex multi-org Salesforce environment requiring centralised Data Cloud
- Ongoing managed services or OPS engagement (not just implementation — the pod model is designed to outlast the project)
- Clients where cross-functional alignment between IT and MarCom is the core delivery risk

**Architecture patterns directly reusable:**
- Dedicated Data Cloud org as hub with Data Spaces for isolation + cross-org collaboration
- BigQuery as identity resolution pre-processing layer (cost management for consumption-based Data Cloud)
- Single Marketing Cloud org with BUs for multi-brand/multi-sector governance
- MuleSoft as the standardised API layer for all downstream Data Cloud consumers
- CI/CD pipeline for Data Cloud metadata (treat Data Cloud like a codebase, not a configuration tool)
- Semantic layer + business dictionary for Data Cloud (business user adoption is the #1 implementation risk)
- Campaign factory approach: reusable Journey Builder templates + self-service tooling to reduce IT dependency for campaign activation

**6-use-case CDP framework** (data sources → data management → unified profiles → activation → intelligence → security) is a complete RFP response structure reusable for any CDP implementation partner bid.

## Lessons Learned

- The bid was lost; the NEOM investment programme was subsequently curtailed. The architecture and delivery model remain sound — the outcome reflects external factors, not solution quality.
- The BigQuery pre-processing recommendation (run transforms before Data Cloud, not inside it) is the most practically impactful cost management insight and should be included in all Data Cloud scoping conversations.
- Business adoption is the real implementation challenge — the document's emphasis on myTrailhead custom trails, campaign factory tooling, and self-service segmentation reflects this; technical implementation is the easier half.
- The semantic layer (descriptions, business rules, data lineage in a business-friendly dictionary dynamically populated by the CI/CD pipeline) is what separates a usable Data Cloud from an unusable one for non-technical marketers.
- Multi-org Salesforce environments should be resolved to a single Data Cloud hub before identity resolution begins — attempting cross-org identity resolution without a centralised hub produces fragmented golden records.

## Related Pages

- [[data-360]] — Data Cloud platform; Data Spaces, identity resolution, segmentation, BYOM
- [[mulesoft]] — API gateway layer; bi-directional sync, REST/ANSI SQL access
- [[marketing-cloud]] — activation layer; Journey Builder, Personalization, Intelligence, BU governance
- [[cross-cloud-data-models]] — multi-org SoR ownership, Data Cloud as analytics layer
- [[cross-cloud-identity]] — Salesforce Identity for unified SSO across NEOM sector portals
- [[gilead-marketing-intelligence-2026]] — comparable scale of Salesforce Data Cloud as commercial intelligence hub
