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
