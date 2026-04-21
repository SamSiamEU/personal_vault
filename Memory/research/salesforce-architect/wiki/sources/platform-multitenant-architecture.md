---
title: Platform Multitenant Architecture
type: source
format: article
url: raw/Platform Multitenant Architecture  Get Started with Fundamentals.md
author: Steve Bobrowski, Tom Leddy (Salesforce)
date_published: 2024-01-01
date_ingested: 2026-04-21
tags: [multitenant, platform, metadata, apex, governor-limits, udd, mt-data]
---

# Platform Multitenant Architecture

## Summary
Technical deep-dive into Salesforce's multitenant, metadata-driven architecture. Explains the Universal Data Dictionary (UDD), MT_Data flex column storage, MT_Indexes/Unique_Indexes/Fallback_Indexes pivot tables, metadata caching, Apex compilation model, bulk processing engine, governor limits rationale, and the Recycle Bin mechanism. The foundational reference for understanding how Salesforce achieves multitenancy at scale.

## Key Takeaways
- MT_Objects + MT_Fields = schema metadata; MT_Data = actual data (all tenants in one table, isolated by OrgID)
- Flex columns (Value0...ValueN) = universal variable-length string storage; platform converts to typed values at query time
- MT_Indexes: typed indexed pivot table (StringValue, NumValue, DateValue) used by custom query optimizer
- Partition pruning: native DB partitioning by OrgID — queries only touch relevant org's data partitions
- Metadata caches: MRU caches for compiled Apex, metadata, and query statistics; avoid disk I/O recompilation
- Custom query optimizer uses pre-queries + multitenant-aware statistics (user-level and group-level selectivity) — not standard cost-based optimizer
- Bulk processing engine: all internal steps execute in bulk; partial-save mode identifies and removes fault records iteratively
- Governor limits: CPU, DML, SOQL, callouts, heap — protect shared multitenant resources; promote efficient coding
- Recycle Bin: IsDeleted soft-delete; 15-day restore window; cascades through master-detail relationships

## Notable Quotes / Data Points
- "The platform does not create an actual table in a database or compile any code. Instead, the platform simply stores some metadata"
- Governor limits "promote better coding techniques among developers and create a better experience for everyone"
- 75% code coverage required before production deployment; unit tests rerun on every platform release

## Wiki Pages Updated
- [[salesforce-platform]] — Multitenant architecture, MT_Data model, governor limits, bulk processing
- [[async-processing-patterns]] — Governor limits context

## Gaps / Follow-up
- MT_Data schema evolution (adding fields to existing objects) process not detailed — impacts large data volume migrations
