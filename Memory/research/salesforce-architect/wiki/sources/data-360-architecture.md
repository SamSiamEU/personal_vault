---
title: Data 360 Architecture
type: source
format: article
url: raw/Data 360 Architecture  Data 360 and Integration.md
author: Salesforce Architect
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [data-360, lakehouse, dmo, dlo, identity-resolution, segmentation, iceberg]
---

# Data 360 Architecture

## Summary
Comprehensive technical reference for Data 360's full architecture stack. Covers the lakehouse foundation (Iceberg/Parquet on Hyperforce), real-time low-latency storage (NVMe LLS), DLOs and DMOs, incremental compute engine (SNCE/CDF), 270+ connectors, identity resolution (deterministic + probabilistic), segmentation types (standard/real-time/waterfall), activation pipelines, the Hyper unified query engine, and BYOM/BYOLLM capabilities.

## Key Takeaways
- Lakehouse on Apache Iceberg/Parquet enables both analytics and AI workloads on the same data
- DLOs are append-only, schema-flexible raw storage; DMOs are canonical semantic objects (200+ standard types)
- SNCE/CDF replaces full-refresh ETL with serverless incremental compute for DLO→DMO transformation
- 270+ connectors span Salesforce clouds, cloud storage (S3, Azure Blob, GCS), warehouses (Snowflake, BigQuery), streaming (Kinesis, Kafka), and legacy systems
- Identity resolution creates Unified Individual/Golden Record via configurable deterministic + probabilistic rules
- Three segmentation types with different latency/freshness profiles (standard → real-time → waterfall)
- Hyper query engine provides unified SQL across all DMOs at sub-second latency
- BYOM/BYOLLM enables custom model inference within Data 360 governance boundary
- Data Graphs: pre-joined relationship maps for agent reasoning and data discovery

## Notable Quotes / Data Points
- Real-time layer uses NVMe LLS for sub-millisecond access — optimized for live agent decisions
- Waterfall segmentation provides priority-ordered audience evaluation (complex marketing use case)
- Calculated Insights available for real-time agent actions — pre-computed metrics ready for instant consumption

## Wiki Pages Updated
- [[data-360]] — Comprehensive architecture overview, all capabilities
- [[agentforce]] — Data 360 as grounding layer (DMOs, vector store, RAG, real-time insights)

## Gaps / Follow-up
- Data Graphs architecture details not fully covered — worth deeper research for agent grounding use cases
- BYOM/BYOLLM configuration and governance specifics (model versioning, trust layer integration) not detailed
