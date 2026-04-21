---
name: Salesforce Integration Patterns (Classic)
type: concept
category: integration-pattern
tags: [integration, api, patterns, callout, remote-process, data-sync, virtualization]
sources: 1
last_updated: 2026-04-21
---

# Salesforce Integration Patterns (Classic)

## Definition
Six canonical integration patterns for connecting Salesforce with external systems, covering process integration (Salesforce initiates or receives calls), data synchronization, and virtual data access. The authoritative Salesforce reference for integration pattern selection.

## When to Use
Use the pattern selection matrix when starting any Salesforce integration project. Match the integration intent (Process/Data/Virtual) and execution timing (Synchronous/Asynchronous) to find the right pattern.

## How It Works

### Pattern Selection Matrix

**From Salesforce to External System:**
| Intent | Timing | Pattern |
|--------|--------|---------|
| Process | Sync | Remote Process Invocation — Request and Reply |
| Process | Async | Remote Process Invocation — Fire and Forget |
| Data | Sync | Remote Process Invocation — Request and Reply |
| Data | Async | UI Update Based on Data Changes |
| Virtual | Sync | Data Virtualization |

**From External System to Salesforce:**
| Intent | Timing | Pattern |
|--------|--------|---------|
| Process | Sync | Remote Call-In |
| Process | Async | Remote Call-In |
| Data | Sync | Remote Call-In |
| Data | Async | Batch Data Synchronization |

### Six Patterns in Detail

#### 1. Remote Process Invocation — Request and Reply
- **Scenario**: Salesforce calls external system, waits for synchronous response, updates Salesforce record
- **Best solution**: External Services (declarative, OpenAPI 3.0/YAML) or Lightning + Apex callout
- **Use case**: Order creation in ERP; payment gateway; real-time credit check
- **Gotcha**: Apex callouts from triggers must be async (@future/Queueable)

#### 2. Remote Process Invocation — Fire and Forget
- **Scenario**: Salesforce triggers external process, doesn't wait for completion
- **Best solution**: Flow-driven Platform Events / Pub/Sub API (gRPC); Good = custom PE; Fit = outbound messaging; Suboptimal = async Apex callouts
- **Platform Event publish behaviors**: "Publish After Commit" (default — rolls back on transaction failure) vs "Publish Immediately" (publishes regardless of transaction outcome); use "Publish Immediately" for audit/notification events where you want the event to persist even if the transaction rolls back
- **72-hour replay window**: High-volume Platform Events replayable for 72 hours; GAP events (shard availability gaps) and Overflow events (exceeded limits) are edge cases requiring monitoring
- **OmniStudio Integration Procedures**: server-side stateless orchestration; chain HTTP Actions / DataRaptor / Set Values with conditional branching, pagination, timeouts, retries, caching; invocable as "integration façades" via REST without requiring Experience Cloud
- **Use case**: Kick off provisioning, send notification, trigger warehouse system

#### 3. Batch Data Synchronization
- **Scenario**: Bulk data movement in either direction on a schedule
- **Best solution**: ETL tool as hub (Salesforce as spoke); Bulk API 2.0 required for middleware ETL; Batch Apex for Salesforce-to-external scheduled exports
- **ETL hub pattern**: control tables track sync state; CDC on source for delta detection; chain/sequence ETL jobs for dependencies; group child records by parent key to avoid DML locking
- **Bulk API 2.0**: parallel-only (no serial mode); each batch is separate transaction; returns 200 HTTP — inspect body for failures; ~2K+ records threshold for Bulk API over REST
- **Use case**: Nightly ERP sync, daily data warehouse load, weekly data cleanup

#### 4. Remote Call-In
- **Scenario**: External system creates/reads/updates/deletes Salesforce data
- **Best solutions by volume/use case**:
  - REST API: standard CRUD; 200 records per call
  - Composite API: 25 requests/call; always returns HTTP 200 — **inspect body, not status code**; 2K+ records → Bulk API 2.0
  - Bulk API 2.0: parallel-only; each batch separate transaction; no serial mode
  - Pub/Sub API (gRPC): preferred for real-time event publishing into Salesforce
  - Platform Events: 100K/250K per hour limits; 72-hour replay
  - SOAP API: legacy; Enterprise/Partner WSDL
  - Apex web/REST services: custom endpoints for specialized logic
- **Session timeout**: 120s for queries
- **Use case**: ERP pushes order updates; external portal creates leads; ETL tool loads accounts

#### 5. UI Update Based on Data Changes
- **Scenario**: Salesforce UI must reflect external data changes in near-real time (without page refresh)
- **Best solution**: Platform Events + CometD/Bayeux (JavaScript library as static resource); Apex Trigger/Flow publishes event; Lightning component subscribes via CometD
- **72-hour replay**: Events available for replay even if consumer was offline; no delivery/ordering guarantee; **Bulk API changes do NOT trigger events** — only API/UI/Apex changes
- **PushTopic pattern**: older approach for subscribing to specific record changes via Streaming API
- **Use case**: Payment confirmation display, case closed notification, live case queue

#### 6. Data Virtualization
- **Scenario**: Salesforce displays or modifies external data without replicating it
- **Best solution**: Salesforce Connect with OData 2.0/4.0 adapter, cross-org adapter (uses REST API directly), or custom Apex adapter (Connector Framework)
- **External Object relationship types**: Lookup (18-char SF record ID), External Lookup (External ID standard field on external object), Indirect Lookup (custom external ID + unique field on standard/custom object)
- **OData paging**: server-driven (external system controls page sizes) vs client-driven (OData adapter controls); max 2,000 rows/page regardless; **High Data Volume option** bypasses most rate limits
- **120s timeout**: same as all other Apex callout patterns; external system must respond in time
- **External objects available via**: SOQL, SOSL, Metadata API, AppExchange packages, global search, list views, page layouts, Lightning mobile
- **Request & Reply is suboptimal**: real-time but requires custom page/button; higher code maintenance
- **Use case**: Display ERP inventory on Opportunity; real-time pricing from external catalog; cross-org data mashup

### Middleware Terminology Reference
Key terms relevant to integration architecture decisions:
- **Event handling**: Pub/Sub capability; route events to active subscribers
- **Protocol conversion**: Middleware converts protocols; Salesforce doesn't natively convert — middleware or endpoint handles
- **Process choreography**: Asynchronous, autonomous; no central controller
- **Service orchestration**: Synchronous, centralized controller coordinates services
- **Transactionality**: Salesforce is transactional within itself but cannot participate in distributed transactions — complex multi-system transactions must be managed at middleware layer

## Key Constraints
- Salesforce Apex synchronous callout timeout: 120 seconds — external APIs must respond within this limit
- Can't make synchronous callouts from trigger context — must use async patterns
- Complex orchestrations should be in middleware (MuleSoft), not Apex — Salesforce timeout values and governor limits make it unsuitable for long-running transaction coordination
- Data Virtualization has performance trade-offs — every field display triggers a real-time call to external system

## Related Patterns / Alternatives
- [[async-processing-patterns]] — Async Apex patterns used to implement Fire-and-Forget and Batch Sync
- [[data-360-integration-patterns]] — Modern Data 360-specific patterns for data ingestion and activation
- [[mulesoft]] — Recommended middleware layer for complex orchestrations and process choreography

## Dennis's Take
External Services + Flow is the best default for new Salesforce integrations that need synchronous callouts — it's declarative, version-controlled, and doesn't require custom Apex. For complex orchestrations spanning multiple systems, put the logic in MuleSoft, not Apex. Apex is for Salesforce-specific logic, not integration orchestration.

## Sources
- [[salesforce-integration-patterns-classic]] — Complete pattern reference with full implementation details, selection matrices, solution options, security appendix, EDA appendix
