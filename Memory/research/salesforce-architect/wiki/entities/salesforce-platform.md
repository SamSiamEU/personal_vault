---
name: Salesforce Platform
type: entity
category: salesforce-cloud
tags: [salesforce, hyperforce, multitenant, metadata-driven, platform]
sources: 3
last_updated: 2026-04-21
---

# Salesforce Platform

## What It Is
The Salesforce Platform is a multitenant, metadata-driven cloud platform that underlies all Salesforce applications. Originally launched in 2008 as Force.com, it has evolved through Hyperforce (cloud-native infrastructure on public clouds), lakehouse data capabilities (Data 360), and native AI/agentic features (Agentforce). As of Dreamforce 2024, 95%+ of Salesforce customers have migrated to the Hyperforce-based platform.

## Relevance to Architecture Work
Understanding the platform's foundational architecture — multitenancy model, metadata-driven customization, governor limits, sharing model — is essential for any Salesforce architect. These fundamentals constrain what agents can do (governor limits on Apex actions), how data access works (sharing model, OWD), and how the platform scales (partitioned MT_Data, indexed MT_Indexes).

## Key Capabilities

### Multitenant Architecture
- **Universal Data Dictionary (UDD)**: MT_Objects, MT_Fields, MT_Data, MT_Indexes — all tenant data in shared tables, isolated by OrgID
- **Flex columns (Value0...ValueN)**: Canonical string storage; platform converts to typed data via SQL functions
- **MT_Indexes**: Pivot table with typed indexed columns (StringValue, NumValue, DateValue) — custom query optimizer uses these for selectivity
- **Data partitioning by OrgID**: Native DB partitioning enables "partition pruning" — queries only touch relevant org's data
- **Metadata caches**: MRU caches for compiled Apex and metadata avoid disk I/O; first execution loads into cache for all org users

### Platform Development
- **Apex**: Java-like language compiled to metadata; enforces governor limits (CPU, DML, SOQL, callouts) to protect multitenancy
- **SOQL/SOSL**: Salesforce Object Query Language (single-object) and Search Language (multi-object, full-text)
- **Flow Builder**: Low-code automation; recommended over Apex for most process automation
- **Bulk API**: Efficient for large data operations; partial-save and all-or-nothing modes
- **Standard APIs**: REST, SOAP, Metadata API, Streaming API (Pub/Sub), Bulk API

### Hyperforce Infrastructure
- **Cloud-native**: Deployed on AWS (primarily), with support for Azure/GCP; multi-AZ per region with 3+ AZ replication
- **Hyperforce Instances/Cells/Supercells**: Scale units with blast radius boundaries; a Cell ≈ traditional "Salesforce instance"
- **Operating Zones**: Grouped Hyperforce Instances for data residency requirements (e.g., EU Operating Zone)
- **Zero-trust security**: mTLS between services, just-in-time access, PKI with certificate revocation, short-lived private keys
- **Blue/green deployments**: Minimize maintenance windows to ~1 minute/year

### Sharing Model
- **OWD (Organization-Wide Defaults)**: Lock records to most restrictive level; all sharing opens up from here
- **Role Hierarchy**: Managers inherit subordinate access; keep to ≤10 levels; ≤5,000 roles (Spring '21+ orgs)
- **Sharing Rules**: Owner-based (300/object) and criteria-based (50/object); no Apex needed for common scenarios
- **Public Groups**: Collections of users/roles/territories; ≤5 nesting levels; ≤100,000 groups per org
- **Apex Managed Sharing**: Programmatic sharing for scenarios not covered by declarative tools
- **Territory Management**: Matrix hierarchy for multi-team account access; maintain separately from role hierarchy
- **Implicit sharing**: Automatic account/contact access based on opportunity/case ownership — non-configurable

### Metadata-Driven Architecture
- **API First**: Every platform action accessible via API — same surface for UI and integrations
- **AppExchange**: 10,000+ apps, 14.3M installs (Oct 2025); 2nd Gen Packaging (2020); Data 360 vector search for app discovery
- **Validation rules, formula fields, roll-up summaries**: Declarative business logic in metadata

### SalesforceDB
- PostgreSQL-derived; compute/storage separation; Kubernetes orchestration; 3 AZ replication
- LSM data structure: append-only transaction log + immutable storage; zero-downtime schema operations
- 1.1 trillion transactions/month; horizontal scaling; tenant ID as part of primary key

### Search as a Service (SeaS)
- Built on Solr; ~6,000 nodes globally; compute/storage separation
- Milvus vector store for semantic/embedding-based search; learning-to-rank
- Agentic Search capabilities for AI-driven retrieval

### AIOps Agent
- Merlion ML ensemble: Isolation Forests + Random Forests + LSTM for anomaly detection
- 91% proactive detection rate; 79% auto-resolution rate
- XGenOps (fine-tuned LLM on operational data) for triage routing; saves 2,800 engineering hours/week

### Availability Architecture
- 10 standards: redundancy+failover, blast radius limits, compartmentalization, auto-scaling, fast rollbacks, load-shedding/WAF, soft dependencies (caching), async communication, fault-tolerant API calls (timeout/circuit-breaker/retry/backoff), service quota management
- 250,000 production changes/week; blue/green with canary + staggered rollout

## Licensing / Pricing
Enterprise/Performance/Unlimited editions have different sharing rule limits and governor limits. API access included in most editions; data storage and API call volume limits vary.

## Strengths
- Battle-tested multitenancy — hundreds of thousands of orgs running concurrently at scale
- Metadata-driven architecture enables customization without code and 3-release-per-year upgrades without downtime
- Deeply integrated security model (OWD → roles → sharing rules) that handles most enterprise access patterns declaratively

## Weaknesses / Gaps
- Governor limits can be painful for complex agent actions — synchronous callout limits, SOQL limits in bulk contexts
- Sharing recalculation for large orgs (2M+ accounts) can be extremely resource-intensive
- Legacy "pilot" features sometimes persist in docs alongside GA features — requires careful version checking

## Known Gotchas
- Data skews: parent records with 10,000+ child records trigger performance issues in sharing recalculation
- Ownership skews: users owning 10,000+ records should be placed at top of role hierarchy or out of role hierarchy
- Account hierarchy does NOT provide data access — parent/child account relationships don't cascade sharing
- OWD changes require sharing recalculation — plan carefully for large orgs
- Apex in trigger context cannot make synchronous callouts — must use @future or Queueable for callouts from triggers

## Sources
- [[platform-multitenant-architecture]] — MT_Data model, UDD, flex columns, query optimizer, governor limits
- [[platform-sharing-architecture]] — OWD, role hierarchy, sharing rules, teams, territory management, Apex sharing, troubleshooting
- [[salesforce-platform-transformed-tomorrow]] — SalesforceDB, AIOps, SeaS, availability architecture, Hyperforce evolution, 6 architectural principles, platform layers, Customer Zero
