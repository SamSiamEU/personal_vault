---
name: Cross-Cloud Data Models
type: concept
category: architecture-pattern
tags: [cross-cloud, data-models, systems-of-record, commerce-cloud, marketing-cloud, service-cloud, data-ownership]
sources: 3
last_updated: 2026-04-21
---

# Cross-Cloud Data Models

## Definition
The framework for assigning clear data ownership ("systems of record") across multiple Salesforce clouds in a multi-cloud deployment. Each cloud owns the data it was designed to manage — no cloud duplicates another's authoritative data. Cross-cloud data access happens via APIs and integration connectors, not replication.

## When to Use
- Any multi-cloud Salesforce deployment (typically Sales/Service + Marketing + Commerce combinations)
- When defining integration architecture: knowing which cloud owns what prevents integration debates and data consistency issues
- When designing compliance architecture: consent, PII, and engagement suppression ownership must be clear

## How It Works

### Systems of Record by Cloud

| Cloud | Owns | Does NOT Own |
|-------|------|-------------|
| Sales / Service Cloud | Person attributes (name, address, demographics), consent/preferences, support cases, opportunities/accounts | Engagement history, ecommerce transactions |
| Marketing Cloud | Engagement history (opens, clicks, unsubscribes), suppression lists, journey state, send history | Profile attributes, order data |
| Commerce Cloud | Ecommerce transactions, order history, cart/wishlist, payment profiles, product affinity | Profile attributes, support history |
| Data 360 | Unified analytical identity, segmentation, behavioral analytics | Live transactional records (these stay in their SoR clouds) |

### Primary Key Architecture
- **Salesforce Contact Record ID** = universal primary key across all clouds
- All clouds reference the Contact ID for the same customer — no cloud issues its own independent customer identifier
- Enables cross-cloud reporting (e.g., "orders for contacts in Segment X") without full data replication

### Integration Connectors (Accelerators)
- **B2C Commerce → Service Cloud Connector**: syncs order data to Service Cloud; agents see order context on Contact/Account record in console
- **B2C Commerce → Marketing Cloud Connector**: syncs catalog + order + customer data to MC data extensions; hooks for post-purchase journeys, cart abandonment, behavioral triggers
- **Marketing Cloud Connect**: replicates CRM objects (Contacts, Leads, Campaigns) to MC; triggers journeys from CRM record updates; surfaces MC email engagement back to CRM Activity Timeline

### Data 360 Layer (Post-Winter '22 Addition)
- Data 360 sits above the transactional SoR layer as the analytics/AI unification layer
- Ingests data from all SoR clouds → unifies into DMOs → resolves identity → enables segmentation and AI grounding
- Does NOT replace SoR ownership — transactional writes still go to the authoritative cloud
- Data 360 is read/analytics layer; SoR clouds are write/operational layer
- **Zero Copy Access from Commerce Cloud** (roadmap, GA ~Q2-Q3 2026): query Commerce data in Data Cloud without physically copying it — eliminates storage duplication cost; Commerce remains the write SoR, Data Cloud queries it in place

### Consent Model Evolution (Roadmap)
- **Unified Consent** (SFCC roadmap): Commerce Cloud will capture consent natively and respect it across all channels with a "common consent model"
- **Current best practice**: consent lives in CRM (Sales/Service Cloud); MC suppression lists are operational enforcement
- **Tension**: Unified Consent suggests Commerce Cloud may become a consent capture point — architectural question: does CRM remain the authoritative SoR for consent, or does a shared consent service emerge?
- Until GA, maintain existing pattern: CRM as consent SoR

### Heroku as Aggregation Layer (Legacy Pattern)
- Pre-Data 360: Heroku was used to aggregate data from multiple clouds into a unified 360° profile API
- Heroku Connect for bi-directional Salesforce CRM sync
- **Now largely superseded** by Data 360 DMOs for new deployments — Data Cloud provides the aggregation layer natively

## Key Constraints
- **No replication without a clear owner**: when data exists in two clouds, define which is authoritative; the other is a derived copy
- **Consent lives in CRM (Sales/Service Cloud)**: not in Marketing Cloud, not in Commerce Cloud — critical for GDPR compliance. MC suppression lists are operational enforcement, not the SoR
- **Winter '22 vintage**: the solution kit patterns are from 2021 — test against current connector versions and Data 360 availability before implementing

## Related Patterns / Alternatives
- **[[cross-cloud-identity]]**: governs how the same customer is *recognized* across clouds; cross-cloud data models govern what *data* each cloud holds
- **[[data-360]]**: the unification layer that ingests from all SoR clouds for analytics and AI — complements, does not replace, SoR ownership
- **[[salesforce-integration-patterns]]**: Remote Call-In and Batch Data Sync patterns are the underlying mechanisms for connector data flows

## Dennis's Take
The SoR ownership framework is the right starting point for any multi-cloud architecture conversation. The hard part in practice is consent: clients often assume Marketing Cloud "owns" the customer relationship and want suppressions managed there. The correct answer is that consent lives in CRM (and should be the GDPR-authoritative record), while Marketing Cloud enforces suppressions operationally. Data 360 changes the game for analytics — the Heroku aggregation layer pattern is dead for new builds; use Data Cloud DMOs instead.

## Contradictions / Open Questions
- Winter '22 connectors: are B2C → Service Cloud and B2C → MC Connector still the recommended approach, or have they been superseded by Data 360 activation patterns?
- Real-time data actions (Data 360 activation): does this replace the SFTP-based MC data feed for order-triggered emails?
- B2B Commerce data model (Account-based): SoR ownership differs — Account vs. Contact as primary entity; not covered in Winter '22 kits

## Sources
- [[cross-cloud-data-models-solution-kit]] — Full SoR framework, connector patterns, Marketing Cloud Connect, Heroku aggregation layer
- [[transactional-email-solution-kit]] — SFTP data feed from Commerce → MC as concrete implementation of the Commerce Cloud SoR feeding MC
- [[sfcc-roadmap]] — Zero Copy Access (Commerce → Data Cloud), Unified Consent, Commerce & Marketing Journeys; updates Winter '22 patterns
