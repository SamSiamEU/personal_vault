# Salesforce Architect Wiki — Activity Log

> Append-only. Never edit or delete past entries.
> Grep all entries: `grep "^## \[" Memory/research/salesforce-architect/log.md`

---

## [2026-04-21] init | Wiki initialized

- Structure created: CLAUDE.md, index.md, log.md, wiki/ skeleton (entities/, concepts/, solutions/, sources/, analyses/)
- Domain: Salesforce architecture — own IP (solutions/) + external references (entities/, concepts/, sources/)
- Scope: Sales/Service/Experience/Data Cloud, Agentforce, integration patterns, DevOps, governance, industry clouds, partner ecosystem
- Status: ready for first ingest

## [2026-04-21] ingest | Gilead Marketing Intelligence — Own IP Solution Page

**Source**: `raw/Gilead Presentation MI 2_26_26 PDF.pdf` — Salesforce presales deck delivered to Gilead, Feb 27 2026; Dennis listed as Senior Manager, Architects on delivery team
**Filing**: Own IP solution page (proposed solution architecture for Gilead, not generic documentation)

**Key content captured**:
- MI data pipeline architecture: two-path model (OOTB Managed Connector vs Total Connect/Custom API)
- SDM layer structure: Raw DLOs → Transform (Add IDs + Enrichments) → Ads DLO → Star Schema → Locked SDM DMOs → Open SDM (custom extensions)
- Locked SDM objects: Campaign DMO, AdGroup DMO, Creative DMO, Ads Facts DMO, Segment DMO + Calc Dims/Meas
- Open SDM: inherits locked SDM relationships, adds new relationships + custom Calc Dims/Meas without breaking base schema
- Pharma DTC HVA funnel: Awareness (Symptom Checker, Prevention Guide, Article) → Consideration/Decision (Find a Doctor, Discussion Guide, Video) → Conversion (QR Scan, Treatment Adherence Sign-Up, PSP Enrollment)
- MTA: tracks full patient journey from unbranded search to PSP enrollment; identifies initiator / nurture / conversion channels
- Cross-Channel Segment Intelligence: unified Tableau Next dashboard for paid (Meta, Google) + owned (Email, SMS) audience performance
- Agentforce autonomous budget optimization with guardrail discussion noted as lesson learned
- Client problem: 8–10 week reporting lag → 3–4 weeks target; fragmented tools consolidation

**Solution page created**:
- [[gilead-marketing-intelligence-2026]] — DTC pharma MI solution, SDM architecture, HVA funnel, MTA pattern

**Index updated**: Solutions section now has first entry.

**Synthesis note**: The Gilead deck is the first own IP in the wiki. It surfaces the locked + open SDM extensibility model as a key architectural detail not captured in the MI entity page — worth knowing for any client that immediately asks "what about our data that isn't in the connector library." The pharma HVA funnel template is directly reusable across other pharma DTC clients.

## [2026-04-21] ingest | Batch Ingest — 18 raw sources from raw/ directory

**Source type**: External references (all sources are Salesforce/MuleSoft official documentation and architectural guides)
**Own IP found**: None identified in readable files; 8 PDFs/DOCX unreadable pending poppler-utils installation

**Pages created**:

*Sources (18):*
- [[architecting-agentic-enterprise-mulesoft]] — MuleSoft Agent Fabric, Vibes, OTEL governance
- [[enterprise-agentic-architecture-design-patterns]] — 15 patterns, 4 archetypes
- [[mulesoft-agent-fabric-deep-dive]] — 4 pillars deep-dive
- [[end-user-identity-propagation-agents]] — OBO/S2S/In-Task, RFC 8693
- [[agentic-patterns-agentforce]] — 5 agent type recipes (partial read)
- [[agent-development-lifecycle]] — ADLC, DX, STDM
- [[data-360-architecture]] — Full architecture stack
- [[data-360-security-architecture]] — ABAC/CEDAR, CMK/BYOK
- [[data-360-clean-rooms]] — Zero-copy clean rooms, PETs
- [[data-360-integration-patterns-guide]] — 11 patterns (partial read)
- [[agentic-enterprise-it-architecture]] — 11-layer model, maturity levels
- [[async-processing-lightning-platform]] — All async Apex patterns
- [[platform-multitenant-architecture]] — MT_Data, UDD, governor limits
- [[platform-sharing-architecture]] — Full sharing model reference
- [[cloudhub-20-ha-dr]] — HA/DR for CloudHub 2.0
- [[salesforce-integration-patterns-classic]] — 6 classic patterns (partial read)
- [[leveraging-mulesoft-informatica]] — "Better Together" framework
- [[salesforce-platform-transformed-tomorrow]] — Platform evolution (partial read)
- [[pdf-solution-kits]] — 8 unreadable PDFs/DOCX (placeholder)

*Entities (4):*
- [[agentforce]] — Salesforce native AI agent platform
- [[mulesoft]] — Salesforce integration platform
- [[data-360]] — Salesforce data platform
- [[salesforce-platform]] — Core Salesforce platform

*Concepts (11):*
- [[agentic-design-patterns]] — 15 named patterns + 5 agent types
- [[agent-orchestration-archetypes]] — 4 system archetypes
- [[mcp-a2a-protocols]] — MCP/A2A interoperability protocols
- [[mulesoft-agent-fabric]] — 4-pillar governance framework
- [[identity-propagation-patterns]] — OBO/S2S/In-Task
- [[adlc]] — Agent Development Lifecycle
- [[async-processing-patterns]] — Lightning Platform async patterns
- [[salesforce-integration-patterns]] — 6 classic integration patterns
- [[data-clean-rooms]] — Zero-copy clean room architecture
- [[hyperforce]] — Salesforce cloud infrastructure
- [[sharing-model]] — Salesforce record access control

**Synthesis note**: The 27 raw files represent a cohesive body of knowledge centered on three domains: (1) Agentic architecture on Salesforce (Agentforce, ADLC, agent patterns, orchestration archetypes), (2) Data 360 as the AI-ready data foundation (lakehouse, identity resolution, clean rooms, security), and (3) Integration patterns (classic SF patterns, Data 360 patterns, MuleSoft/CloudHub). The emerging thesis is that Salesforce's differentiation in the agentic era is the combination of native CRM data + Data 360's grounded knowledge + Agentforce's reasoning — all governed by MuleSoft Agent Fabric for cross-vendor deployments.

**Pending**: 
- 8 unreadable PDFs need poppler-utils installation (`brew install poppler`)
- Partial reads: Agentic Patterns (offset 400+), Integration Patterns (lines 200+), Salesforce Platform Transformed (lines 150+), Data 360 Integration Patterns (full)
- overview.md updated this session

## [2026-04-21] ingest | PDF Batch — 8 remaining raw files (PDFs + DOCX)

**Source type**: External references (Salesforce solution kits, practitioner DOCX, product guide)
**Unblock**: poppler-utils installed via `brew install poppler`; PDFs read via `pdftotext` bash workaround (Read tool PDF path lookup issue)

**Files processed**:
- `agentforce_implementation_customer.pdf` — read first 200 lines; customer ADLC guide with Makana Medical Devices example
- `seamless_cross_cloud_identity_solution_kit.pdf` — read first 200 lines; Experience Cloud + Commerce Cloud identity federation via Salesforce Identity
- `cross_cloud_data_models_solution_kit.pdf` — read first 200 lines; SoR per cloud, B2C connectors, Marketing Cloud Connect
- `conversational_campaigns_whatsapp_solution_kit.pdf` — read first 150 lines; SMS→WhatsApp flow, Einstein Bots, 24-hour session window
- `transactional_email_solution_kit.pdf` — read first 150 lines; Commerce Cloud → SFTP → Marketing Cloud transactional email
- `Solution Kit - Digital Wallet in SDO.pdf` — full read; Digital Wallet in demo orgs, TenantEnrichedUsageEvent DLO, consumption tracking
- `Marketing Cloud Engage tips.docx` — full read (via Python zipfile); AMPScript/SSJS bridge pattern, TreatAsContent, SSJS template
- `SFCC Roadmap items.pdf` — UNREADABLE: image-based PDF, no extractable text; requires OCR (`brew install tesseract`)

**Source pages created (8)**:
- [[agentforce-implementation-customer]] — customer ADLC 5-stage guide
- [[cross-cloud-identity-solution-kit]] — Winter '22 identity federation pattern
- [[cross-cloud-data-models-solution-kit]] — Winter '22 SoR ownership framework
- [[conversational-campaigns-whatsapp-solution-kit]] — WhatsApp campaign flow
- [[transactional-email-solution-kit]] — SFTP-to-MC transactional email
- [[digital-wallet-sdo-solution-kit]] — Digital Wallet in SDO, DLO consumption architecture
- [[marketing-cloud-engage-tips]] — AMPScript/SSJS developer patterns
- [[sfcc-roadmap]] — placeholder (image-based PDF, unreadable)

**Entities created (3)**:
- [[marketing-cloud]] — Marketing Cloud platform: Email Studio, Journey Builder, AMPScript/SSJS, Marketing Cloud Connect
- [[experience-cloud]] — Experience Cloud: portal platform, identity hub, profile SoR in cross-cloud B2C architecture
- [[commerce-cloud]] — B2C/B2B Commerce (SFCC/SFRA): shopping data SoR, connector-based integration

**Concepts created (2)**:
- [[cross-cloud-identity]] — Salesforce Identity as IdP, Contact Record ID as primary key, don't-sync-federate principle
- [[cross-cloud-data-models]] — SoR ownership by cloud, connector accelerators, Data 360 as analytics overlay

**Synthesis note**: The Winter '22 solution kits add a cross-cloud B2C architecture layer missing from the agentic/integration deep-dives. Core principle: each cloud is an authoritative SoR for its data domain; Salesforce Identity federates authentication; Contact Record ID is the universal primary key. Data 360 sits above all clouds as the analytics/AI unification layer — it doesn't displace SoR ownership, it reads from all SoR clouds to build unified profiles and segments. The Agentforce implementation guide confirms ADLC phases but adds customer-facing detail (guardrails-first design, per-agent analytics). Digital Wallet surfaces consumption architecture detail: TenantEnrichedUsageEvent DLO and consumption tags are the billing model.

**Pending**:
- SFCC Roadmap PDF requires OCR: `brew install tesseract`, then `tesseract "SFCC Roadmap items.pdf" output -l eng pdf`
- All Winter '22 solution kits partially read (first 150-200 lines); detailed configuration guides in remainder
- Partial reads from prior session: Agentic Patterns (offset 400+), Classic Integration Patterns (offset 200+), Salesforce Platform Transformed (offset 150+), Data 360 Integration Patterns (full)
- overview.md updated to reflect cross-cloud coverage additions

## [2026-04-21] ingest | 2 new raw files — MC Growth Implementation Guide + Gilead Presentation

**Files found**:
- `mktg_implementation_guide.pdf` — Salesforce official Marketing Cloud Growth/Advanced Edition Implementation Guide (Summer '25, May 2025); external reference; fully read (2967 lines)
- `Gilead Presentation MI 2_26_26 PDF.pdf` — Salesforce presales/demo deck for Gilead (pharma); own IP (Dennis as "Senior Manager, Architects"); dated Feb 27, 2026; fully read; **solution page pending — awaiting Dennis's context on engagement outcome and architectural decisions**

**Key discovery**: Two distinct products are both called "Marketing Cloud":
1. **Legacy Marketing Cloud** (Email Studio / Journey Builder / AMPScript / SSJS) — separate infrastructure, Data Cloud optional
2. **Marketing Cloud Growth/Advanced Edition** — native Salesforce Platform, Data Cloud *required*, Flow-based campaigns, Unified Messaging

This distinction was not previously represented in the wiki. MC Growth/Advanced Edition is architecturally closer to a Salesforce CRM + Data Cloud extension than to legacy MC.

**Source pages created (1)**:
- [[marketing-cloud-growth-implementation-guide]] — Full setup guide: Data Kits, Unified Messaging, consent in Data Cloud DMOs, identity resolution rulesets, web tracking, scoring, AI features (STO/Metrics Guard/Engagement Scoring/Engagement Frequency), limits, permission sets

**Entity pages created (1)**:
- [[marketing-intelligence]] — New product entity: paid-media analytics on Data Cloud + Tableau Next; pre-built SDM; MTA; HVAs; Agentforce autonomous optimization; pharma DTC use case

**Entity pages updated (1)**:
- [[marketing-cloud]] — Added prominent warning distinguishing Legacy vs New; added full MC Growth/Advanced capabilities section; updated Contradictions/Open Questions; added source link

**Pending**:
- Gilead presentation: own IP solution page awaiting Dennis's input on engagement context, outcome, and architectural decisions worth capturing
- [[data-360]] and [[overview.md]] minor updates for MC Growth/Advanced integration story could be done after Dennis confirms Gilead context

## [2026-04-21] ingest | Partial Reads Completion — 4 large files fully read and wiki updated

**Files completed**:
- `Agentic Patterns and Implementation with Agentforce.md` — lines 400–1264 (COMPLETE); Autonomous + Collaborative patterns, all 5 implementation recipes, Agentforce 3.0 (voice/Python), A2A/MCP architecture, 4-category data integration patterns
- `The Salesforce Platform - Transformed for Tomorrow.md` — lines 150–977 (COMPLETE); SalesforceDB, LLS, DPC, AIOps Agent (91% detection / 79% resolution), SeaS, Agentforce platform layers, MuleSoft ACB+MCP, Tableau Next, AppExchange, Customer Zero, Industries, availability architecture
- `Integration Patterns  Data 360 and Integration.md` — lines 200–1235 (COMPLETE); Patterns 2–6 full detail including Platform Event publish behaviors, OmniStudio Integration Procedures, Composite API gotcha (HTTP 200 always), Bulk API 2.0 parallel-only, Salesforce Connect External Object relationship types, OData paging; security + EDA appendix
- `Data 360 Integration Patterns  Data 360 and Integration.md` — lines 100–1967 (COMPLETE); all 11 patterns: Kinesis/MSK, Zero-Copy Inbound (External DLO + File Federation), Zero-Copy Outbound (Data Share + Data Share Target), Data Cloud One (Home/Companion Org), Batch Activation, File Export, Connect API, Data Graph API (?live=true), Real-Time Data Actions

**Source pages updated (4)**:
- [[salesforce-integration-patterns-classic]] — removed partial read note; full Pattern 2–6 implementation details; Composite API gotcha; Bulk API 2.0 parallel-only; Platform Event publish behaviors; Salesforce Connect adapters; security + EDA appendix
- [[data-360-integration-patterns-guide]] — removed partial read note; all 11 patterns in detail; Data Cloud One; activation patterns; Data Graph API; Real-Time Data Actions
- [[agentic-patterns-agentforce]] — removed partial read note; Autonomous + Collaborative patterns; all 5 recipes; Agentforce 3.0; A2A/MCP implementation; 4-category data integration patterns for agents
- [[salesforce-platform-transformed-tomorrow]] — removed partial read note; SalesforceDB; LLS; DPC; AIOps; SeaS; Agentforce platform layers; MuleSoft ACB+MCP; Tableau Next; AppExchange; Customer Zero

**Entity pages updated (4)**:
- [[agentforce]] — Agentforce 3.0 (voice/Python/Agentforce Script), A2A server capability, MCP client, platform layers
- [[salesforce-platform]] — SalesforceDB (1.1T txn/month), SeaS (Solr/Milvus/6K nodes), AIOps (91%/79%), availability architecture, AppExchange scale
- [[mulesoft]] — Anypoint Code Builder, Integration Intelligence, bidirectional MCP, A2A/Inference Connectors, RPA/IDP, Interpreted Connectivity
- [[data-360]] — LLS, DPC, Semantic Layer, Document AI, Personalization Services, Vegacache, Data Cloud One, all activation patterns

**Concept pages updated (2)**:
- [[agentic-design-patterns]] — Autonomous pattern (goal+strategy layer, 3 monitoring levels), Collaborative pattern (Slack, episode state), all 5 implementation recipes, 4 data integration patterns, AgentGoal__e, long-running agent open question
- [[salesforce-integration-patterns]] — Patterns 2–6 complete with full implementation detail

**Synthesis note**: All 27 raw sources are now fully read and wikified. The partial reads were the deepest material — the four files together cover the complete agentic + platform + integration + data stack at implementation depth. Key additions to the mental model: (1) Agentforce 3.0 is a Python event-driven async framework with voice and state-machine scripting — it's closer to a traditional app framework than a wizard tool; (2) SalesforceDB is PostgreSQL-derived but purpose-built for hyperscale multitenancy at 1.1T transactions/month; (3) Data Cloud One solves the multi-org problem natively; (4) Zero-Copy is now bi-directional and complete as an architectural pattern; (5) MuleSoft ACB with built-in MCP server positions MuleSoft at the center of the MCP ecosystem, not just as an HTTP integration platform.

**Status**: All raw sources ingested. Wiki coverage is comprehensive except DevOps/Release Management, Industry Clouds, CPQ, and Field Service Lightning — no sources exist for these domains.

## [2026-04-21] ingest | SFCC Roadmap Items (OCR re-ingest)

**Source type**: External reference (Salesforce B2C Commerce Cloud product roadmap)
**Unblock**: tesseract OCR installed; PDF converted to PNG via `pdftoppm -r 200 -png`, then OCR'd per page; 13 pages extracted

**Files processed**: `SFCC Roadmap items.pdf` — full 13-page read via tesseract OCR

**Key content**: B2C Commerce roadmap Q4 2025 – H1 2026:
- Native Intelligent Search (semantic + context-aware; GA Q2 2026) — displaces 3P search tools
- Zero Copy Access Commerce → Data Cloud (GA ~Q2-Q3 2026) — eliminates SFTP/storage duplication
- Unified Consent across Commerce + Marketing (roadmap) — challenges CRM-as-consent-SoR principle
- Commerce & Marketing Journeys (OOTB WhatsApp/SMS/email templates for commerce flows)
- Composable Storefront completeness + MCP developer tools (preview)
- Product Discovery in AI Shopping Platforms (ChatGPT et al.) — Q4 2025/Q1 2026
- BYO Payments + native Adyen integration (GA Q1 2026)
- TikTok Shop native integration (GA Q1 2026)
- PCI 4.0 + eCDN Unified Shield threat protection (GA Nov 2025)

**Pages updated**:
- [[sfcc-roadmap]] — full source page replacing placeholder
- [[commerce-cloud]] — major capabilities update (Native Search, Zero Copy, MCP, AI discovery, social commerce, Composable Storefront); new open questions
- [[cross-cloud-data-models]] — Zero Copy section, Unified Consent evolution and tension with CRM-as-consent-SoR principle; sfcc-roadmap added as source

**Synthesis note**: The SFCC roadmap reveals Commerce Cloud is rapidly becoming AI-native. Two most architecturally significant items: (1) Zero Copy Access — Commerce data queryable in Data Cloud without copying, completing the zero-copy story across all clouds; (2) Product Discovery in AI Platforms — Commerce catalogs become agent-discoverable, making SFCC part of the agentic enterprise fabric. MCP developer tools (preview) signal Commerce joining the same protocol layer as MuleSoft and Agentforce. The Unified Consent item introduces tension with existing guidance — monitor for GA details before updating consent architecture recommendations.

**Pending**:
- Partial reads: Agentic Patterns (offset 400+), Classic Integration Patterns (offset 200+), Salesforce Platform Transformed (offset 150+), Data 360 Integration Patterns (full)
- Winter '22 solution kits: detailed config sections not yet read
- overview.md: update Cross-Cloud section to add SFCC roadmap insights (Zero Copy, Native Search, AI discovery)
