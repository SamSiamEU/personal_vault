---
title: Asynchronous Processing on the Lightning Platform
type: source
format: article
url: raw/Asynchronous Processing on the Lightning Platform  Get Started with Fundamentals.md
author: Salesforce Architect
date_published: 2024-01-01
date_ingested: 2026-04-21
tags: [apex, async, queueable, batch, platform-events, cdc, scheduled]
---

# Asynchronous Processing on the Lightning Platform

## Summary
Comprehensive reference for all async processing patterns on the Salesforce Lightning Platform. Covers Future Methods, Queueable Apex, Batch Apex, Scheduled Apex, Platform Events, Change Data Capture, and Bulk API. Includes a comparison table of capabilities, limits, retry behaviors, and use case guidance. Also covers flow control mechanisms and fair usage limits that protect the multitenant environment.

## Key Takeaways
- @future: primitives only, no chaining, 50 per transaction — legacy pattern; Queueable is strictly better
- Queueable: complex types, chainable (up to 5 levels), good for agent action post-processing
- Batch Apex: up to 50M records; governor limits reset per chunk; 5 concurrent max per org; not suitable for real-time agent responses
- Scheduled Apex: cron-like; max 100 scheduled jobs per org
- Platform Events: 72-hour replay buffer; pub/sub decoupling; CometD for external subscribers; 250K publishes per 24h (default)
- CDC: Near-real-time change events for all field changes on subscribed objects; same 72h replay buffer; powers Data 360 SNCE incremental sync
- Bulk API 2.0: Up to 150M records; for external ETL loads and data migrations
- Fair use: elastic limits protect all tenants; monitor Async Apex queue depth

## Notable Quotes / Data Points
- Platform Events and CDC replay buffer = 72 hours — critical for integration reliability during outages
- Batch Apex chunk size configurable up to 2,000 records — tune for performance vs. governor limit margin

## Wiki Pages Updated
- [[async-processing-patterns]] — Full pattern comparison, limits, use case guidance
- [[salesforce-platform]] — Governor limits context for multitenancy

## Gaps / Follow-up
- Exact Platform Events per-org limits vary by edition — verify for client-specific designs
- Interaction between Platform Events and Data 360 streaming connectors (CDF pattern) could be documented more clearly
