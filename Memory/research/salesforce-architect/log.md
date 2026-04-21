# Salesforce Architect Wiki — Activity Log

> Append-only. Never edit or delete past entries.
> Grep all entries: `grep "^## \[" Memory/research/salesforce-architect/log.md`

---

## [2026-04-21] init | Wiki initialized

- Structure created: CLAUDE.md, index.md, log.md, wiki/ skeleton (entities/, concepts/, solutions/, sources/, analyses/)
- Domain: Salesforce architecture — own IP (solutions/) + external references (entities/, concepts/, sources/)
- Scope: Sales/Service/Experience/Data Cloud, Agentforce, integration patterns, DevOps, governance, industry clouds, partner ecosystem
- Status: ready for first ingest

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
