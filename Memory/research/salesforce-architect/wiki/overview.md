# Salesforce Architect Wiki — Overview

> Master synthesis. The evolving answer to: *"What do I know about Salesforce architecture, and where does my own practice stand?"*
> Not an index — a living memo. Updated when new ingests meaningfully shift the picture.
> Last updated: 2026-04-21 (post full ingest of all 27 raw sources)

---

## Current Thesis

Salesforce's architectural differentiation in the agentic era is the combination of three tightly integrated layers: **native CRM data** (system of record), **Data 360** (AI-ready data platform that unifies and grounds agents in enterprise knowledge), and **Agentforce** (the reasoning and action layer). Together, these form a closed loop no single competitor can fully replicate. For cross-vendor deployments, **MuleSoft Agent Fabric** extends this with governance that enforces identity, policy, and observability across any AI platform combination.

The platform is transitioning from _application-centric_ (apps own data and logic) to _agent-first_ (agents dynamically compose capabilities from modular services and governed data). Architects who design for this shift — not around it — define the next decade of enterprise software delivery.

---

## Own IP — Pattern Library

*(No solutions filed yet. Populated from `wiki/solutions/` as Dennis's own work is ingested.)*

---

## Domain Coverage

### Agentic Architecture
**Well covered** after batch ingest:
- [[agentic-design-patterns]] — 15 named patterns, 5 agent types, implementation recipes for each type
- [[agent-orchestration-archetypes]] — SOMA/MOMA/Multi-Vendor A2A — the system-level topology decisions
- [[adlc]] — Full lifecycle from ideation to production monitoring; invest in Phase 5 (tuning) from day one
- [[mcp-a2a-protocols]] — MCP (agent-to-tool) and A2A (agent-to-agent): practical vs. governance-mature split

**Starting points for client work**: Greeter → Operator → Orchestrator as default architecture. Map business requirements to 5 agent types before jumping to implementation. ADLC Phase 5 must be designed in sprint 1.

### Integration
**Well covered**:
- [[salesforce-integration-patterns]] — Canonical 6-pattern reference; selection matrix by intent × timing
- [[async-processing-patterns]] — All Lightning Platform async patterns; Platform Events as the cleanest default
- [[identity-propagation-patterns]] — OBO/S2S/In-Task for agent identity through call chains
- [[mulesoft-agent-fabric]] — 4-pillar governance framework for multi-vendor agent ecosystems
- [[cloudhub-ha-dr]] (via [[mulesoft]] entity) — Active-active with Route 53 for enterprise MuleSoft SLAs

**Gaps**: Data 360 Integration Patterns guide (partial read — patterns 2-11 need full review); Classic patterns 2-6 details

**Key principle**: Orchestration logic belongs in MuleSoft, not Apex. Apex for Salesforce-specific logic only.

### Data Architecture
**Well covered**:
- [[data-360]] — Full architecture: lakehouse, DLO/DMO, identity resolution, segmentation, BYOM, ABAC
- [[data-clean-rooms]] — Zero-copy clean room model, PETs, Salesforce implementation, activation gap solution
- [[sharing-model]] — Complete record access model; OWD-first design philosophy

**Gaps**: Data Cloud One multi-org architecture; CEDAR policy language specifics; Semantic Layer / EKG product mapping

**Key insight**: Data quality upstream is the #1 dependency for everything downstream — segmentation accuracy, clean room match rates, AI agent grounding. Address before promising outcomes.

### Platform Fundamentals
**Well covered**:
- [[salesforce-platform]] — MT architecture, governor limits, sharing model, bulk processing
- [[hyperforce]] — Infrastructure model, zero-trust, Operating Zones for data residency, US East control plane dependency

**Gaps**: Platform Transformed guide partially read (lines 150+) — Metadata Framework evolution, AI layer details

### DevOps & Release Management
**Not yet covered** — no sources ingested on CI/CD, SFDX, scratch orgs, Copado/Gearset/Flosum.

### Governance & Security
**Well covered**:
- [[data-360-security-architecture]] — ABAC/CEDAR, OLS/FLS/RLS, CMK/BYOK, compliance certifications
- [[hyperforce]] — Zero-trust infrastructure, end-to-end encryption, phishing-resistant MFA

**Gaps**: AppSec/code scanning, org security patterns, compliance frameworks in practice

### Cross-Cloud Architecture (B2C)
**Covered** (Winter '22 solution kits — foundational patterns):
- [[cross-cloud-identity]] — Salesforce Identity as IdP; Experience Cloud as profile SoR; Commerce Cloud as shopping SoR; don't-sync-federate principle; Contact Record ID as universal primary key
- [[cross-cloud-data-models]] — SoR ownership by cloud; B2C connector accelerators; Marketing Cloud Connect; Data 360 as analytics overlay
- [[commerce-cloud]] — B2C/B2B Commerce (SFCC/SFRA); shopping data SoR; SFTP connector pattern
- [[marketing-cloud]] — Email Studio, Journey Builder, AMPScript/SSJS; Marketing Cloud Connect; cross-cloud engagement execution layer
- [[experience-cloud]] — Portal platform; identity hub; customer profile SoR in B2C architecture

**Starting points for client work**: Always assign SoR ownership per cloud before designing integrations. Consent lives in CRM (Sales/Service Cloud). Data 360 is the analytics/AI layer above all SoRs — it reads from them, never replaces them. The Heroku aggregation pattern is dead for new builds.

**SFCC Roadmap updates the picture** (Q4 2025–H1 2026):
- **Zero Copy Commerce → Data Cloud**: Commerce data queryable in Data Cloud without copying — completes the zero-copy story across all Salesforce clouds. Eliminates the need for SFTP data feeds for analytics use cases.
- **Native Intelligent Search** (GA Q2 2026): semantic + context-aware search ends the 3P search tool debate. For new implementations, defer Algolia/Coveo investment.
- **Product Discovery in AI Platforms** (Q4 2025–Q1 2026): Commerce catalogs indexed for ChatGPT, Perplexity et al. Commerce Cloud entering the agentic ecosystem.
- **MCP developer tools for Composable Storefront** (preview): Commerce joining the same MCP protocol layer as MuleSoft and Agentforce.
- **Unified Consent** (roadmap): Commerce will capture consent natively — **watch this**: tensions with CRM-as-consent-SoR principle. Do not change consent architecture until GA details are clear.

**Gaps**: Winter '22 solution kits are foundational but pre-Data 360 — validate connector patterns against current stack. No B2B Commerce-specific cross-cloud patterns.

### Industry Clouds
**Not yet covered** — no sources ingested on FSC, Health Cloud, Manufacturing Cloud, Nonprofit.

---

## Open Questions

1. **Enterprise Orchestration Layer product mapping**: The 11-layer model describes this as the "control plane for end-to-end work." Which specific Salesforce/MuleSoft product implements this at Maturity Level 3+? Is it MuleSoft Agent Broker? Agentforce Orchestrator? Something not yet GA?

2. **Agentforce native agent identity**: How does Agentforce handle agent-to-agent identity propagation for SOMA/MOMA patterns *without* MuleSoft? Is there an equivalent of Flex Gateway OBO inside Salesforce?

3. **CEDAR policy language**: ABAC/CEDAR is the authorization model for Data 360. What does writing CEDAR policies look like in practice? Are they configured declaratively in Data Cloud UI or programmatically?

4. **Long-running autonomous agents**: Token expiry, state persistence, and rollback semantics for agents that span hours or days are not documented. What's the architectural pattern for a 3-day procurement workflow agent?

5. **Data Cloud One**: How does multi-org federation handle conflicting DMO schemas? What's the governance model when two orgs define "Customer" differently?

6. **Unified Consent (SFCC roadmap)**: The SFCC roadmap says Commerce Cloud will have a "common consent model" across Commerce and Marketing. Does this create a new consent SoR, a consent sync mechanism, or just enforced propagation? Does CRM remain the GDPR-authoritative consent record?

7. **Guided Shopping Agent**: The SFCC roadmap references a "guided shopping agent" powered by the new Contextual Search. Is this an Agentforce-based product? A Commerce-embedded agent? New product name?

---

## Where Knowledge Is Thin

| Area | Status | Notes |
|------|--------|-------|
| DevOps & Release Management | Not started | No sources yet on CI/CD, scratch orgs, Copado |
| Industry Clouds | Not started | FSC, Health, Manufacturing, Nonprofit |
| CPQ & Revenue Cloud | Not started | No sources yet |
| Field Service Lightning | Not started | No sources yet |
| Marketing Cloud Engage | Covered | AMPScript/SSJS patterns; strategic architecture still thin |
| Commerce Cloud (SFCC) | Covered | Winter '22 cross-cloud patterns; SFCC roadmap needs OCR |
| SFCC Roadmap PDF | Covered | OCR'd via tesseract; full 13-page roadmap ingested |
| Autonomous agent patterns | Partial | agentic-patterns-agentforce only read to line 400 |
| Real-Time Data Actions (Data 360) | Partial | Integration patterns guide only read 100 lines |
| Agentforce pricing/licensing | Thin | Consumption-based; Digital Wallet DLO architecture known; per-unit rates unclear |
| Cross-cloud (B2B Commerce) | Thin | Winter '22 kits cover B2C; B2B account-based patterns not covered |
| Marketing Cloud strategic architecture | Thin | Scripting patterns covered; MCOPS/platform evolution not covered |
