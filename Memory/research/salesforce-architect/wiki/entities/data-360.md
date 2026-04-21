---
name: Data 360
type: entity
category: salesforce-cloud
tags: [data-360, data-cloud, cdp, lakehouse, identity-resolution, segmentation]
sources: 5
last_updated: 2026-04-21
---

# Data 360

## What It Is
Data 360 (formerly Salesforce Data Cloud / Customer 360 Data Platform) is Salesforce's cloud-native data platform built on a lakehouse architecture. It provides unified customer profiles, real-time segmentation, AI/ML capabilities, and activation pipelines across the Salesforce ecosystem and external platforms. It runs on Hyperforce and supports petabyte-scale data management with open table formats (Iceberg/Parquet).

## Relevance to Architecture Work
Data 360 is the data foundation for every serious Salesforce architecture today. It's the semantic layer between CRM data and AI agents (RAG retrievers, vector store), the source for personalization in Marketing Cloud, and the integration hub for enterprise data via 270+ connectors. For agentic architectures, Data 360's DMOs, vector stores, and real-time insights are what ground Agentforce agents in trusted enterprise data.

## Key Capabilities

### Data Architecture
- **Lakehouse foundation**: Apache Iceberg/Parquet on Hyperforce; open table formats; petabyte-scale
- **Low Latency Store (LLS)**: NVMe SSD petabyte-scale durable cache between memory and lakehouse; real-time layer for sub-second event processing
- **Data Processing Controller (DPC)**: JaaS (Jobs as a Service) across Spark/KRC; supports BYOC (Java/Python/Spark)
- **Semantic Layer**: Declarative query language across DMOs; abstract SQL joins for analysts and agents
- **Document AI**: Invoice/resume/unstructured document processing integrated into the data platform
- **Personalization Services Platform**: A/B/n testing and multi-arm bandit optimization for real-time personalization
- **Vegacache**: Redis-based cache layer; 2 trillion requests/day; sub-millisecond latency
- **Data Lake Objects (DLOs)**: Schema-flexible raw data storage; append-only, preserves source fidelity
- **Data Model Objects (DMOs)**: Canonical semantic layer with 200+ standard objects; the join surface for agents and analytics
- **Data Spaces**: Logical tenant isolation within one org — scoped by region, regulation, or partnership; shared across orgs via Data Cloud One
- **SNCE/CDF**: Serverless incremental compute for DLO → DMO transformation; replaces full-refresh ETL
- **270+ connectors**: Direct connectors to Salesforce clouds, AWS S3, BigQuery, Snowflake, Kinesis, Kafka, and more
- **Zero-copy federation (inbound)**: External DLO is a metadata pointer; query pushdown to Snowflake/Databricks; File Federation via Apache Iceberg/Delta Lake direct from S3/ADLS/GCS
- **Zero-copy sharing (outbound)**: Data Share → Data Share Target; external warehouse queries Data 360 DMOs/CIOs as read-only views via Snowflake/Databricks; bi-directional zero-copy loop complete

### Identity & Profiles
- **Identity resolution**: Deterministic + probabilistic matching rules; creates Unified Individual (Golden Record)
- **Data Graph API**: Pre-joined real-time JSON representation of complete 360° customer profile
- **Unified query engine (Hyper)**: SQL across all DMOs with sub-second latency

### AI/ML Layer
- **Vector store**: Stores embeddings for RAG retrieval by Agentforce agents
- **RAG retrievers**: Connect agents to unstructured knowledge (docs, articles, policies)
- **BYOM/BYOLLM**: Bring your own model or LLM for custom inference
- **Calculated/Streaming/Real-time Insights**: Pre-computed metrics available for real-time agent decisions and personalization

### Segmentation & Activation
- **Standard segmentation**: Batch audience builder on DMOs
- **Real-time segmentation**: Streaming-based; updates audiences as signals arrive
- **Waterfall segmentation**: Priority-ordered segment evaluation
- **Activation targets**: Marketing Cloud, Meta Ads, Google Ads, ad networks, external platforms, clean rooms
- **Batch Activation**: Segment → Activation → MC Shared Data Extensions, ad platforms, CRM; consent-aware; idempotency key = Segment ID + Activation ID + Target System ID
- **File Export Activation**: Segment → S3/Azure Blob/GCS/SFTP as CSV/Parquet/JSON; for compliance archival, external ML, BI
- **Data Graph API**: GET /api/v1/dataGraph/{entity}/{id}; pre-materialized denormalized JSON; ?live=true for real-time vs cached; sub-second; for real-time decisioning and personalization
- **Real-Time Data Actions**: Sub-second activation triggered by signals; CEDAR policy at PDP; synchronous (offer token) or async orchestration; rate limiting required
- **Data Cloud One**: Home Org + Companion Orgs model; Data Spaces shared explicitly; no custom code; near-real-time sync

### Security
- **Hyperforce zero-trust**: Data never leaves Salesforce boundary without explicit policy
- **ABAC/CEDAR**: Attribute-based access control with PIP/PDP/PEP triad at runtime
- **OLS/FLS/RLS/DDM**: Object/field/row-level security + dynamic data masking
- **CMK/BYOK**: Customer-managed encryption keys; bring your own key
- **Einstein Trust Layer**: PII masking for LLM calls; zero-data-retention guarantees

### Clean Rooms
- **Zero-copy clean room architecture**: Federation model — data stays at source, only compliant aggregated results shared
- **Privacy-Enhancing Technologies (PETs)**: Differential privacy, aggregation thresholds, result suppression
- **Audit DMO**: Immutable audit trail for every clean room query
- **Native Salesforce-to-Salesforce** and **cross-cloud (AWS Clean Rooms)** collaboration models

## Licensing / Pricing
Consumption-based credit model. Credits consumed by: rows processed, query complexity, identity resolution operations (higher multiplier), batch ingestion (lower multiplier). Digital Wallet tracks real-time consumption.

## Strengths
- Only Salesforce-native platform that unifies CRM + external data at petabyte scale
- Native grounding layer for Agentforce agents via RAG and real-time insights
- ABAC/CEDAR is more granular and dynamic than traditional RBAC — suitable for AI workload governance
- Clean room capability natively embedded — no separate vendor needed

## Weaknesses / Gaps
- Data quality matters enormously — poor identity resolution degrades match rates for clean rooms and AI
- Real-time segmentation and waterfall segmentation have different latency profiles; choosing wrong type causes UX issues
- BYOM/BYOLLM requires MLOps investment to maintain model lifecycle outside Salesforce

## Known Gotchas
- Zero-copy doesn't eliminate compute costs — federation still triggers compute at source; query patterns must be optimized
- Data Spaces are scoped per org; a Data Space cannot span multiple orgs (requires Data Cloud One or separate setup)
- ABAC/CEDAR enforcement applies at query time via the PEP; agents must be provisioned with correct attribute claims

## Contradictions / Open Questions
- Boundary between Data 360 and Salesforce CRM data platform in post-Agentforce architecture is still evolving (some features overlap)

## Sources
- [[data-360-architecture]] — Comprehensive architecture overview: lakehouse, real-time layer, DMOs, SNCE, identity resolution, segmentation, Hyper
- [[data-360-security-architecture]] — Hyperforce zero-trust, ABAC/CEDAR, OLS/FLS/RLS, CMK/BYOK, AWS PrivateLink
- [[data-360-clean-rooms]] — Zero-copy clean room model, PETs, audit trail, use cases across industries
- [[data-360-integration-patterns-guide]] — Complete 11-pattern reference: all ingestion, zero-copy, Data Cloud One, all activation patterns
- [[agentic-patterns-agentforce]] — Data 360 as grounding layer: RAG, vector store, Calculated Insights API, Data Graph, streaming insights
- [[salesforce-platform-transformed-tomorrow]] — LLS, DPC, Semantic Layer, Document AI, Personalization Services, Vegacache
