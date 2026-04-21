---
title: Integration Patterns (Salesforce Classic Reference)
type: source
format: article
url: raw/Integration Patterns  Data 360 and Integration.md
author: Salesforce Architect
date_published: 2024-01-01
date_ingested: 2026-04-21
tags: [integration, patterns, callout, remote-process, data-sync, batch, virtualization]
---

# Integration Patterns (Salesforce Classic Reference)

## Summary
The canonical Salesforce integration pattern reference covering 6 integration archetypes: Remote Process Invocation (Request-Reply and Fire-and-Forget), Batch Data Synchronization, Remote Call-In, UI Update Based on Data Changes, and Data Virtualization. Includes a pattern selection matrix (intent × timing) and a middleware terminology reference. This is the reference document used by Salesforce consulting architects for integration design reviews.

## Key Takeaways
- Six patterns cover all major integration scenarios; selection matrix maps intent (Process/Data/Virtual) × timing (Sync/Async) to pattern
- **External Services** (declarative, OpenAPI 3.0) is the best solution for most new synchronous callouts from Salesforce — no custom Apex needed
- Apex callouts from triggers must be async (@future/Queueable) — synchronous callouts from trigger context not allowed
- Complex orchestrations should be in middleware (MuleSoft), not Apex — governor limits and timeout values make Salesforce unsuitable for multi-system transaction coordination
- Data Virtualization (External Objects / Salesforce Connect): real-time access to external data without replication; performance trade-off — every display triggers a call
- Salesforce is transactional within itself but cannot participate in distributed transactions — compensating transactions must be at middleware layer
- Batch Data Sync: Bulk API 2.0 for external → Salesforce; Batch Apex for Salesforce → external scheduled exports

## Notable Quotes / Data Points
- "We recommend that all complex orchestrations be implemented in the middleware layer because of Salesforce timeout values and governor limits"
- Pattern selection matrix: only 5 patterns cover all Salesforce-outbound scenarios; only 4 cover Salesforce-inbound
- Long polling via CometD/Bayeux protocol for UI Update pattern

## Wiki Pages Updated
- [[salesforce-integration-patterns]] — Complete pattern reference and selection matrix
- [[async-processing-patterns]] — Fire-and-Forget and Batch Sync patterns
- [[salesforce-platform]] — Governor limits and transactionality constraints

## Gaps / Follow-up
- Only read first 200 lines — patterns 2-6 need additional reading for full implementation details
- Platform Events as integration pattern (Fire-and-Forget evolution) not covered in this file — covered separately in async-processing doc
