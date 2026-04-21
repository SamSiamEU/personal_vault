---
title: Data 360 Integration Patterns (Modern Guide)
type: source
format: article
url: raw/Data 360 Integration Patterns  Data 360 and Integration.md
author: Salesforce Architect
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [data-360, integration, patterns, ingestion, zero-copy, activation, data-graph]
---

# Data 360 Integration Patterns (Modern Guide)

## Summary
Modern integration pattern guide specifically for Data 360, covering data ingestion (batch and streaming), zero-copy federation (inbound and outbound), unified multi-org data platform (Data Cloud One), and activation patterns (batch segments, file export, on-demand API, real-time data actions). Organized around the same 3-category framework as the classic integration guide (Data/Process/Virtual) with a middleware capability matrix. This is the Data 360-specific evolution of the classic Salesforce integration patterns reference — 11 patterns in full detail.

## Key Takeaways

### Batch Ingestion Patterns
- **Cloud Storage (S3/GCS/Azure)**: 100M rows / 50GB per object limit; `schema_sample.csv` required (headers + 1 data row); strict naming (letters/digits/underscores only); checkpointing for idempotency; partitioning + Append node in Batch Data Transform; Named Credentials + External Credentials; IAM least privilege
- **CRM Connector + MC Engagement Connector**: Starter Data Bundles for standard objects; dedicated integration user with connector permission set; full vs delta refresh modes; OAuth 2.0 Connected App; LastModifiedDate for delta detection; ABAC/CEDAR tagging immediately post-ingestion

### Streaming Ingestion Patterns
- **Ingestion API (event push)**: OAS 3.0 schema strict enforcement; JWT Bearer OAuth; streaming JSON for low-latency vs bulk CSV for large; dead-letter queue for persistent failures; idempotency key required; sub-second to second latency; real-time DMO graph for instant activation
- **Web/Mobile Behavioral Events**: Salesforce Interactions SDK (JS beacon/native); Marketing Cloud Personalization Connector; <2s latency to real-time graph; consent flags (GDPR/CCPA) in SDK; event size 1–5 KB; millions of events/minute capable
- **CDC-based CRM Sync**: CRM Connector with streaming enabled; subscribes to ChangeEvent channels (/data/ContactChangeEvent); durable replay cursors; RecordID+SequenceNumber for idempotency; UPSERT strategy; "Enable Permissions for CRM Streaming" system permission required; hybrid mode (CDC + batch) for unsupported objects
- **AWS Kinesis / MSK Kafka**: Native connectors; IAM (Kinesis) or OIDC (MSK) auth; schema file upload; DLQ replay; PartitionKey+SequenceNumber (Kinesis) or Topic+Partition+Offset (MSK) for exact-once; connector checkpointing; PrivateLink/VPC for secure routing

### Zero-Copy Patterns
- **Zero-Copy Inbound (Data Federation)**: Data 360 creates External DLO (metadata pointer — no copy); query pushdown to Snowflake/Databricks compute; File Federation via Apache Iceberg/Delta Lake bypasses compute (direct S3/ADLS/GCS reads); RBAC at source enforces least privilege; PrivateLink/VPC peering; key-pair/OAuth/OIDC auth; schema drift → Schema Rejection Queue; compliance stays at source
- **Zero-Copy Outbound (Data Sharing)**: Administrator creates Data Share in Data 360 → selects DMOs/CIOs → creates Data Share Target (Snowflake/Databricks account) → publishes → external admin accepts → shared objects appear as read-only views in warehouse; Data Share API for programmatic/MuleSoft access; Iceberg/Parquet option for object storage; all access audited in Trust Layer
- Both Zero-Copy directions form a bi-directional loop: "data stays decentralized, intelligence becomes unified"

### Data Cloud One (Multi-Org)
- **Home Org** = single Data 360 instance (provisioned once); **Companion Orgs** connect via Data Cloud One app with no custom code
- Data Spaces logically segment data (e.g., Retail, Service, Marketing); only selected Data Spaces are shared with each companion org
- Data Cloud One Bridge provisions a Data Cloud One user and applies Permission Sets in companion org
- Companion orgs query data graph, use Einstein/Apex/Flows, and can trigger activations
- Idempotency: Org ID + Record ID + Version Number; conflict resolution = last-write-wins or policy-driven merge; near-real-time sync (seconds)
- Security: mutual OAuth 2.0 with auto-rotated tokens; CEDAR/ABAC policy enforcement; Private Connect optional

### Activation Patterns
- **Batch Activation**: Segment Builder → Activation → select target (MC Engagement, Google Ads, Meta, LinkedIn, CRM, MuleSoft) → payload definition (contact IDs + enrichment attributes) → scheduled export; consent-aware Trust Layer; Shared Data Extensions in MC; composite idempotency key = Segment ID + Activation ID + Target System ID; millions of records per run; checkpoint-based recovery
- **File Export Activation**: Same workflow as batch but outputs CSV/Parquet/JSON to S3/Azure Blob/GCS/SFTP; IAM roles/service principals; checksum validation on write; scheduled or manual; for compliance archival, external ML, BI tools
- **On-Demand Connect API**: OAuth 2.0 Connected App → /services/data/vXX.X/connect endpoints; JSON response; cursor-based pagination; ETag/Last-Modified for caching; foundation for UI-centric portal/mobile apps; combine with Data Graph API for semantic queries; MuleSoft/Apex wrapper option for additional orchestration
- **Data Graph API**: GET /api/v1/dataGraph/{entity}/{id} returns pre-materialized denormalized JSON (multiple DMOs combined); ?live=true bypasses cache for real-time (slightly higher latency); sub-second for cached; single-record lookups (not bulk); circuit breaker on live failure → fallback to cached; ETag for cache validation
- **Real-Time Data Actions**: Sub-second to low-single-second latency; identity resolution (email/externalId/cookie → Unified Individual ID, cache hit path); CEDAR policy enforcement at PDP; edge cache (short TTL); synchronous (return offer token) or async orchestration (queue + webhook); gRPC for ultra-low latency; GraphQL for flexible field selection; Platform Events for fan-out; idempotency key = UUID + client namespace; DLQ for async orchestration failures; rate limiting required

## Notable Quotes / Data Points
- "Choosing the right integration approach is a critical architectural decision, not an implementation detail"
- Data Graph API: "pre-materialized denormalized view — retrievable via single key lookup within milliseconds"
- Zero Copy Outbound: "redefines Data 360 from a data repository to a semantic activation layer"
- Real-Time Data Actions: "turns unified data into in-the-moment intelligence"
- Data Cloud One: "companion orgs can access unified data in minutes, not weeks of custom coding"

## Wiki Pages Updated
- [[data-360]] — Complete integration pattern set: all ingestion, zero-copy, Data Cloud One, activation
- [[cross-cloud-data-models]] — Zero-copy Commerce → Data Cloud pattern (SFCC roadmap alignment)

## Gaps / Follow-up
- Real-Time Data Actions: detailed Flow-based trigger implementation vs. API-direct vs. webhook not distinguished — both appear valid
- Data Cloud One: conflicting DMO schema resolution across orgs with different object definitions not fully documented
