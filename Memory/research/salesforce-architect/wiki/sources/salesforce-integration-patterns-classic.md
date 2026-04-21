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
The canonical Salesforce integration pattern reference covering 6 integration archetypes: Remote Process Invocation (Request-Reply and Fire-and-Forget), Batch Data Synchronization, Remote Call-In, UI Update Based on Data Changes, and Data Virtualization. Includes a pattern selection matrix (intent × timing), middleware terminology reference, security appendix (Named Credentials, OAuth 2.0, Private Connect, WS-*), and an EDA appendix (Platform Events + CDC + Pub/Sub API). This is the reference document used by Salesforce consulting architects for integration design reviews.

## Key Takeaways
- Six patterns cover all major integration scenarios; selection matrix maps intent (Process/Data/Virtual) × timing (Sync/Async) to pattern
- **External Services** (declarative, OpenAPI 3.0) is the best solution for most new synchronous callouts from Salesforce — no custom Apex needed
- Apex callouts from triggers must be async (@future/Queueable) — synchronous callouts from trigger context not allowed
- Complex orchestrations should be in middleware (MuleSoft), not Apex — governor limits and timeout values make Salesforce unsuitable for multi-system transaction coordination
- Data Virtualization (External Objects / Salesforce Connect): real-time access to external data without replication; performance trade-off — every display triggers a live call
- Salesforce is transactional within itself but cannot participate in distributed transactions — compensating transactions must be at middleware layer
- Batch Data Sync: Bulk API 2.0 for external → Salesforce; Bulk API required for ETL middleware tools
- **Pattern 2 (Fire and Forget)**: Best = Flow-driven Platform Events / Pub/Sub API (gRPC); Good = custom PE; Fit = outbound messaging; Suboptimal = async Apex callouts
- **Pattern 2 (Fire and Forget)**: Platform Event publish behaviors — "Publish After Commit" (default, rolls back on failure) vs "Publish Immediately" (publishes regardless of tx outcome); 72-hour event replay window; GAP events and Overflow events are CDC edge cases
- **OmniStudio Integration Procedures**: server-side stateless orchestration; chain HTTP Actions/DataRaptor/Set Values with conditional branching, pagination, timeouts, retries, caching; invocable as "integration façades" via REST
- **Pattern 3 (Batch Data Sync)**: ETL tool as hub, Salesforce as spoke; control tables pattern; CDC on source; group child records by parent key to avoid DML locking; Bulk API 2.0 required for middleware ETL
- **Pattern 4 (Remote Call-In)**: Composite API (25 requests/call, always returns 200 — inspect body for subrequest failures); Bulk API 2.0 parallel-only (no serial mode, each batch separate transaction); Platform Events 100K/250K per hour limits; 200 records per SOAP/REST call; 2K+ records → Bulk API 2.0; session timeout 120s for queries
- **Pattern 5 (UI Update)**: Platform Events + CometD/Bayeux for near-real-time UI notifications; 72-hour replay; no delivery/ordering guarantee; Bulk API changes don't trigger; Apex PushTopic for specific field subscriptions
- **Pattern 6 (Data Virtualization)**: Salesforce Connect as Best; OData 2.0/4.0, cross-org (REST API direct), custom Apex adapter; external objects: Lookup (18-char SF ID), External Lookup (External ID standard field), Indirect Lookup (custom external ID + unique); 120s timeout; OData paging max 2000 rows/page; High Data Volume option bypasses rate limits; External Objects available via SOQL, SOSL, Metadata API, AppExchange

## Notable Quotes / Data Points
- "We recommend that all complex orchestrations be implemented in the middleware layer because of Salesforce timeout values and governor limits"
- Pattern selection matrix: only 5 patterns cover all Salesforce-outbound scenarios; only 4 cover Salesforce-inbound
- Composite API: "The call returns HTTP 200 even if subrequests fail — always inspect the response body, not the HTTP status code"
- Bulk API 2.0: parallel-only mode; each batch is a separate transaction — no serial processing mode available
- EDA appendix: "Platform Events + CDC + Pub/Sub API enables enterprises to create event-driven architectures that decouple message consumers from producers"

## Wiki Pages Updated
- [[salesforce-integration-patterns]] — Complete 6-pattern reference with full implementation details
- [[async-processing-patterns]] — Fire-and-Forget platform event patterns, OmniStudio Integration Procedures
- [[salesforce-platform]] — Governor limits, transactionality, Bulk API behaviors

## Gaps / Follow-up
- Security appendix covers reverse proxy, Shield Platform Encryption, WS-* protocol support — not filed as separate concept page
- EDA appendix is high-level overview only — detailed event bus patterns covered in async-processing-lightning-platform source
