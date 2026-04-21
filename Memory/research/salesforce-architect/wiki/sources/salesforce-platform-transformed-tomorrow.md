---
title: The Salesforce Platform — Transformed for Tomorrow
type: source
format: article
url: raw/The Salesforce Platform - Transformed for Tomorrow  Get Started with Fundamentals.md
author: Salesforce (Chief Architect office)
date_published: 2024-01-01
date_ingested: 2026-04-21
tags: [salesforce-platform, hyperforce, architecture, agentforce, evolution, metadata]
---

# The Salesforce Platform — Transformed for Tomorrow

## Summary
Strategic architectural white paper co-authored with Salesforce's top engineers describing the platform's transformation from Force.com (2008) through Hyperforce to the current AI/agentic platform. Fully read (977 lines). Covers 6 architectural principles, 10 platform layers, Hyperforce, SalesforceDB, Data 360 LLS/DPC/Semantic Layer, AIOps, Agentforce platform layers, SeaS (Search as a Service), MuleSoft ACB with MCP, Tableau Next, AppExchange, Industries, and Salesforce's own "Customer Zero" deployment.

## Key Takeaways

### Platform Architecture
- **6 architectural principles**: Enterprise-Grade Trust, Multitenant, Metadata-Driven, API First, Open and Interoperable, Agentic
- **10 platform layers**: Hyperforce, Metadata Framework, Data, AI, App Platform Services, Business Capabilities, APIs + API Management, User/Dev Experience, Integration, Apps and Industries
- 95%+ of customers migrated to Hyperforce as of Dreamforce 2024
- **Metadata-driven runtime**: Core runtime + ORM with multitenancy; 85,000+ Salesforce entities, 300M+ customer-defined entities; layered extension (SF Engineering → ISVs → IT Admins → End Users); Record Save Order of Execution
- **Apex scale**: 350 billion Apex transactions/month (Oct 2025); 42,000 developers using AI tools monthly, 17.6M lines of code accepted

### Availability Architecture
- **10 availability standards**: Redundancy+failover, blast radius limits, compartmentalization, auto-scaling, fast rollbacks, load-shedding/WAF, soft dependencies (caching), async communication, fault-tolerant API calls (timeout/circuit-breaker/retry/backoff), service quota management
- **CI/CD**: 250,000 production changes/week; blue/green deployment; mandatory testing evidence, canary, staggered rollouts with controlled blast radius, health checks

### SalesforceDB
- PostgreSQL-derived; compute/storage separation; Kubernetes orchestration; 3 AZ replication
- LSM data structure: append-only transaction log + immutable storage
- 1.1 trillion transactions/month; horizontal scaling; tenant ID as part of primary key; zero-downtime schema operations

### Data 360 Platform Layer
- **Low Latency Store (LLS)**: NVMe SSD petabyte-scale durable cache between memory and lakehouse; real-time layer for sub-second event processing
- **Data Processing Controller (DPC)**: JaaS (Jobs as a Service) across Spark/KRC; BYOC (Java/Python/Spark)
- **Semantic Layer**: Declarative query language across DMOs
- **Document AI**: Invoice/resume/unstructured document processing
- **Personalization Services Platform**: A/B/n testing and multi-arm bandit optimization
- **Vegacache**: Redis-based, 2 trillion requests/day, sub-millisecond latency

### AIOps Agent
- Merlion ML ensemble: Isolation Forests + Random Forests + LSTM for anomaly detection
- 91% proactive detection rate; 79% auto-resolution rate; XGenOps (fine-tuned LLM on operational data) for triage routing
- Saves 2,800 engineering hours/week

### SeaS (Search as a Service)
- Built on Solr; ~6,000 nodes globally; compute/storage separation; Milvus for vector search; learning-to-rank; Agentic Search capabilities

### Agentforce Platform Layers (internal)
- AI Platform → AI Foundational Services (AI Gateway/Feedback/RAG/Agentic Orchestration/Agent Evaluation) → Agentforce Studio (Agent Builder/Prompt Builder/Testing Center/Model Builder/Next Gen Authoring)

### MuleSoft Integration Layer
- Named Credentials, External Services (OpenAPI declarative), External Objects, Unified API Catalog
- **Anypoint Code Builder (ACB)**: Next-gen IDE with built-in MCP server; AI-generated integrations; Topic Center for Agentforce actions
- **Integration Intelligence**: Next-gen observability built on Data 360 + Tableau Semantics + Tableau Next
- CloudHub 2.0 / Runtime Fabric / PCE deployment models
- **Bidirectional MCP**: Salesforce as MCP client AND MCP server
- Interpreted Connectivity (non-code integration); RPA and IDP for legacy/document integration
- A2A Connectors and Inference Connectors

### Tableau Next
- VizQL engine; Pulse Metrics layer; built on Agentforce; Tableau Semantics as universal semantic layer
- API-first; native Data 360 integration; proactive AI insights; deep Slack integration

### AppExchange
- 10,000+ apps; 14.3M installs (as of Oct 2025); 2nd Gen Packaging (2020); re-architected search with Data 360 vector search

### Customer Zero
- Salesforce uses its own products ("Customer Zero" philosophy); GUS on Hyperforce since Aug 2020
- 10,000 daily active internal AI tool users; 100+ internal AI agents

### Industries
- Rebuilt on Salesforce Platform; composability across verticals; layered architecture: Platform → horizontal apps → common capabilities → horizontal business logic → domain-specific customizations

## Notable Quotes / Data Points
- "Currently, more than 95% of our customers have transitioned to this new platform"
- "1.1 trillion transactions per month through SalesforceDB"
- "350 billion Apex transactions per month"
- AIOps: "saves 2,800 engineering hours per week through automated detection and resolution"
- "250,000 production changes per week through our CI/CD pipelines"

## Wiki Pages Updated
- [[salesforce-platform]] — SalesforceDB, AIOps, SeaS, availability architecture, metadata-driven details, Apex scale
- [[hyperforce]] — Instances/Cells/Supercells, Operating Zones, zero-trust, FinOps (from initial read — no new additions)
- [[data-360]] — LLS, DPC, Semantic Layer, Document AI, Personalization Services, Vegacache
- [[agentforce]] — Platform layers (AI Foundational Services, Studio layers), Agentforce 3.0 context
- [[mulesoft]] — Anypoint Code Builder, Integration Intelligence, bidirectional MCP, A2A connectors, Interpreted Connectivity

## Gaps / Follow-up
- AIOps Agent uses XGenOps (internal fine-tuned LLM) — relationship to Agentforce/Atlas Reasoning not clarified
- Tableau Next details (VizQL internals, Pulse Metrics architecture) not deeply covered
- Industries composability model (how vertical customizations layer on horizontal business logic) needs further study
