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
Modern integration pattern guide specifically for Data 360, covering data ingestion (batch and streaming), zero-copy federation (inbound and outbound), unified multi-org data platform (Data Cloud One), and activation patterns (batch segments, on-demand API, real-time data actions). Organized around the same 3-category framework as the classic integration guide (Data/Process/Virtual) with a selection matrix. This is the Data 360-specific evolution of the classic Salesforce integration patterns reference.

## Key Takeaways
- **11 specific patterns** organized into: Batch Ingestion, Streaming/Real-Time Ingestion, Zero-Copy (Inbound+Outbound), Unified Multi-Org (Data Cloud One), Activation (Batch + On-Demand API + Real-Time Actions)
- **Batch Ingestion**: Cloud storage (S3/Azure Blob/GCS) → bulk load; or Salesforce Clouds → native connectors + Data Streams
- **Streaming Ingestion**: Ingestion API (event payloads), Web/Mobile SDKs (behavioral data), CRM streaming (near-RT CDC sync), Kinesis/MSK (cloud messaging platforms)
- **Zero-Copy Inbound**: Data 360 queries Snowflake, BigQuery, external datasets without replicating data; governance enforced at source
- **Zero-Copy Outbound**: External systems (Databricks, Tableau) query Data 360 curated segments/insights without replication
- **Data Cloud One**: Unified multi-org platform — connects multiple Salesforce orgs under shared metadata + semantic model without data duplication
- **Activation Patterns**: Batch segments → Marketing Cloud/Meta/Google Ads; On-Demand via Connect API; Real-Time Data Actions triggered by signals
- **Data Graph API**: On-demand retrieval of complete 360° customer profile as pre-joined JSON — for real-time decisioning or personalization
- Selection framework: integration intent (Data/Process/Virtual) × timing (Sync/Async)

## Notable Quotes / Data Points
- "Choosing the right integration approach is a critical architectural decision, not an implementation detail"
- Data Graph API returns "pre-joined, real-time JSON representation of the complete 360° view for decisioning or personalization"
- Real-Time Data Actions: "customer activity signal triggers an instant real-time action — such as updating CRM, invoking Einstein scoring, or launching a retention journey"

## Wiki Pages Updated
- [[data-360]] — Integration patterns for all ingestion/activation scenarios

## Gaps / Follow-up
- Only read first 100 lines (table of contents and selection matrix); full pattern details need further reading (file is 43K tokens)
- Data Cloud One architecture and multi-org setup not fully covered yet
- Real-Time Data Actions implementation mechanics (Flows vs. Apex vs. API webhooks) need additional research
