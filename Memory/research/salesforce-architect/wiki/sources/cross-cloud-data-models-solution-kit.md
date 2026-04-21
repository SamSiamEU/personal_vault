---
title: Cross-Cloud Data Models Solution Kit
type: source
format: pdf
url: raw/cross_cloud_data_models_solution_kit.pdf
author: Salesforce
date_published: 2021-01-01
date_ingested: 2026-04-21
tags: [cross-cloud, data-models, commerce-cloud, marketing-cloud, service-cloud, solution-kit, winter-22]
---

# Cross-Cloud Data Models Solution Kit

## Summary
Winter '22 solution kit defining which Salesforce cloud owns which data — the "systems of record" model for multi-cloud deployments. Provides a framework for resolving data ownership conflicts, describes integration accelerators (B2C connectors), and explains how Marketing Cloud Connect ties CRM data to Marketing Cloud.

## Key Takeaways

### Systems of Record by Cloud

| Cloud | Owns |
|-------|------|
| Sales / Service Cloud | Person attributes (name, address, demographics), consent records, case management, opportunity/account |
| Marketing Cloud | Engagement history, suppression lists, journey flow state, email/SMS preferences |
| Commerce Cloud | Ecommerce transactions, product affinity, cart state, order history, payment methods |

### Primary Key Architecture
- **Salesforce Contact Record ID** = primary key across all clouds
- All clouds reference this ID; no cloud issues its own independent customer ID
- Enables cross-cloud reporting and journey triggering without data duplication

### Integration Accelerators
- **B2C Commerce → Service Cloud Connector**: syncs order data to Service Cloud for case context; enables agents to see order history on Contact/Account record
- **B2C Commerce → Marketing Cloud Connector**: syncs catalog, customer, and order data to Marketing Cloud data extensions; enables post-purchase journeys and behavioral targeting

### Marketing Cloud Connect
- Replicates CRM data (Contacts, Leads, Campaigns) to Marketing Cloud
- Triggers journeys from CRM record updates (e.g., Contact field change → journey entry)
- Exposes MC email engagement data (opens, clicks, unsubscribes) back to CRM Activity Timeline
- Enables CRM-driven segmentation in Marketing Cloud

### Heroku as Aggregation Layer
- When data needs to be combined across clouds in real time (e.g., 360° profile API), Heroku can serve as a data aggregation/orchestration layer
- Heroku Connect for bi-directional Salesforce CRM sync
- Pattern: Heroku microservice reads from multiple SoRs → composes unified view → returns to requestor

## Notable Quotes / Data Points
- Winter '22 (2021) — predates Data 360; with Data 360 now available, Heroku aggregation role is partially superseded by Data Cloud DMOs
- Connector accelerators reduce custom integration effort but have field mapping limitations
- Consent management explicitly lives in Service/Sales Cloud, not Marketing Cloud — important for GDPR compliance architecture

## Wiki Pages Updated
- [[cross-cloud-data-models]] (new concept — to be created)
- [[marketing-cloud]] (new entity — to be created)

## Gaps / Follow-up
- Read first 200 lines (pdftotext); detailed field mapping and connector configuration in remainder
- How does Data 360 DMO architecture supersede or complement this SoR model? Data Cloud DMOs can unify the data — but SoR ownership principles still apply
- B2B Commerce variant (Account-based) has different data model — not covered here
