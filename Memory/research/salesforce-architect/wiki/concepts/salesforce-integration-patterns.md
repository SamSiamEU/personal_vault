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
- **Best solution**: Outbound Messaging (workflow-based) or Apex @future/Queueable
- **Use case**: Kick off provisioning, send notification, trigger warehouse system

#### 3. Batch Data Synchronization
- **Scenario**: Bulk data movement in either direction on a schedule
- **Best solution**: Bulk API 2.0 (external → SF) or Scheduled Apex/Batch Apex (SF → external)
- **Use case**: Nightly ERP sync, daily data warehouse load, weekly data cleanup

#### 4. Remote Call-In
- **Scenario**: External system creates/reads/updates/deletes Salesforce data
- **Best solution**: REST API (CRUD operations), SOAP API (legacy), Bulk API (mass operations)
- **Use case**: ERP pushes order updates; external portal creates leads; ETL tool loads accounts

#### 5. UI Update Based on Data Changes
- **Scenario**: Salesforce UI must reflect changes to Salesforce data in real time (without page refresh)
- **Best solution**: Streaming API / CometD; Lightning Web Components with @wire reactive adapters
- **Use case**: Live case queue; real-time dashboard; collaborative record editing

#### 6. Data Virtualization
- **Scenario**: Salesforce accesses external data in real time without replicating it
- **Best solution**: External Objects (Salesforce Connect) with OData or custom adapter
- **Use case**: Display ERP inventory on Opportunity; show real-time pricing from external catalog

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
- [[salesforce-integration-patterns-classic]] — Complete pattern reference with selection matrices, solution options, trade-offs
