# Salesforce Architect Wiki — Overview

> Master synthesis. The evolving answer to: *"What do I know about Salesforce architecture, and where does my own practice stand?"*
> Not an index — a living memo. Updated when new ingests meaningfully shift the picture.
> Last updated: 2026-04-21 (post batch ingest of 18 raw sources)

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

### Industry Clouds
**Not yet covered** — no sources ingested on FSC, Health Cloud, Manufacturing Cloud, Nonprofit.

---

## Open Questions

1. **Enterprise Orchestration Layer product mapping**: The 11-layer model describes this as the "control plane for end-to-end work." Which specific Salesforce/MuleSoft product implements this at Maturity Level 3+? Is it MuleSoft Agent Broker? Agentforce Orchestrator? Something not yet GA?

2. **Agentforce native agent identity**: How does Agentforce handle agent-to-agent identity propagation for SOMA/MOMA patterns *without* MuleSoft? Is there an equivalent of Flex Gateway OBO inside Salesforce?

3. **CEDAR policy language**: ABAC/CEDAR is the authorization model for Data 360. What does writing CEDAR policies look like in practice? Are they configured declaratively in Data Cloud UI or programmatically?

4. **Long-running autonomous agents**: Token expiry, state persistence, and rollback semantics for agents that span hours or days are not documented. What's the architectural pattern for a 3-day procurement workflow agent?

5. **Data Cloud One**: How does multi-org federation handle conflicting DMO schemas? What's the governance model when two orgs define "Customer" differently?

---

## Where Knowledge Is Thin

| Area | Status | Notes |
|------|--------|-------|
| DevOps & Release Management | Not started | No sources yet on CI/CD, scratch orgs, Copado |
| Industry Clouds | Not started | FSC, Health, Manufacturing, Nonprofit |
| CPQ & Revenue Cloud | Not started | No sources yet |
| Field Service Lightning | Not started | No sources yet |
| Marketing Cloud Engage | Partial | DOCX unreadable; see [[pdf-solution-kits]] |
| Commerce Cloud (SFCC) | Partial | PDF unreadable; see [[pdf-solution-kits]] |
| PDF solution kits (8 files) | Unread | Install poppler-utils: `brew install poppler` |
| Autonomous agent patterns | Partial | agentic-patterns-agentforce only read to line 400 |
| Real-Time Data Actions (Data 360) | Partial | Integration patterns guide only read 100 lines |
| Agentforce pricing/licensing | Thin | Consumption-based model confirmed; rates unclear |
