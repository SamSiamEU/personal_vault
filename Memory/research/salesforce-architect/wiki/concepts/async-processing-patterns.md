---
name: Async Processing Patterns (Lightning Platform)
type: concept
category: architecture-pattern
tags: [apex, async, queueable, batch, platform-events, scheduled, bulk-api]
sources: 1
last_updated: 2026-04-21
---

# Async Processing Patterns (Lightning Platform)

## Definition
Mechanisms for executing long-running, high-volume, or deferred operations on the Salesforce Lightning Platform outside the synchronous transaction context. These patterns are critical for avoiding governor limit violations and for building scalable integrations, automation, and agent actions.

## When to Use
Use async patterns when:
- An operation exceeds synchronous Apex limits (CPU time, callout limits, heap size)
- Processing large record volumes (1,000+ records)
- Operations should run on a schedule (nightly sync, monthly reports)
- Decoupling is required: trigger an event and let subscribers handle the work independently
- Agent actions need to invoke long-running processes without blocking the agent response

## How It Works

### Pattern Comparison

| Pattern | Trigger | Volume | Retry | Use Case |
|---------|---------|--------|-------|----------|
| **Future Methods (@future)** | Explicit call from trigger/Apex | Single record | None | Simple async callout from trigger context |
| **Queueable Apex** | Explicit enqueue; can chain | Small-medium batches | Manual | Chained async operations; passes complex types |
| **Batch Apex** | Scheduled or explicit start | Up to 50M records | Built-in chunking | ETL, data cleanup, bulk processing |
| **Scheduled Apex** | Cron-like schedule | Any | N/A | Periodic maintenance jobs |
| **Platform Events (Pub/Sub)** | DML / publish from Apex/API | High volume | Replay buffer (72h) | Event-driven integration; decoupled subscribers |
| **Change Data Capture (CDC)** | Salesforce record changes | All field changes | Replay buffer | External system sync; agent event feeds |
| **Bulk API 2.0** | External system call | Up to 150M records | N/A | Data migration, ETL, external loads |

### Key Patterns in Detail

#### Queueable Apex
- Can be chained (up to 5 levels deep in production)
- Passes complex objects (unlike @future which only takes primitives)
- Good for agent action results that need multi-step async processing
- Subject to concurrent Queueable job limits — monitor Async Apex queue depth

#### Batch Apex
- Processes records in chunks (default 200, configurable up to 2,000)
- Start, Execute, Finish methods — clean separation of lifecycle
- Governor limits reset per batch chunk
- Use for bulk data operations: nightly sync, data cleansing, backfill operations
- Agent actions should rarely invoke Batch Apex directly — too slow for interactive responses

#### Platform Events
- Publish-subscribe: publishers don't know who's consuming
- 72-hour replay buffer for event recovery
- CometD/Streaming API for external subscribers
- Flow/Apex can subscribe to platform events for event-driven automation
- Best for: integration event bus, agent event feeds (proactive agent patterns), loose coupling

#### Change Data Capture (CDC)
- Publishes change events for every DML on subscribed objects
- External systems (MuleSoft, external databases) subscribe for near-real-time sync
- Same 72-hour replay buffer as Platform Events
- Key for Data 360 incremental sync (SNCE/CDF pattern)

### Fair Use Mechanisms
- Salesforce enforces elastic limits: org-level limits for concurrent Queueable jobs, batch executions
- High-volume Platform Events consumption requires careful monitoring of subscriber lag
- Batch Apex for very large datasets (10M+ records) should use SOQL with size limits and indexed WHERE clauses

## Key Constraints
- @future methods: max 50 per transaction; no chaining; primitives only
- Batch Apex: max 5 concurrent batches per org; 100 active batch jobs in queue
- Platform Events: 250,000 event publishes per 24h (default); retry on subscriber failure requires event replay
- Scheduled Apex: max 100 scheduled jobs per org
- All async processing is eventually consistent — no atomic rollback across Queueable chains

## Related Patterns / Alternatives
- [[agentic-design-patterns]] — Proactive agents often trigger async flows via Platform Events
- [[salesforce-integration-patterns]] — Async patterns are the Salesforce-side of Fire-and-Forget and Batch Data Sync integration patterns

## Dennis's Take
Platform Events are the cleanest async pattern for most integration and agentic use cases — they decouple producers from consumers and have good replay semantics. Use Queueable for complex agent action post-processing. Avoid @future for new code — Queueable is strictly better. Batch Apex is for bulk ETL, not real-time agent actions.

## Sources
- [[async-processing-lightning-platform]] — Full pattern comparison table, Flow control / fair usage mechanisms, governor limits context
