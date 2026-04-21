---
title: Digital Wallet in SDO Solution Kit
type: source
format: pdf
url: raw/Solution Kit - Digital Wallet in SDO.pdf
author: Salesforce
date_published: 2025-11-03
date_ingested: 2026-04-21
tags: [digital-wallet, data-360, agentforce, consumption, billing, finops, sdo, solution-kit]
---

# Digital Wallet in SDO Solution Kit

## Summary
Solution kit (updated November 2025) enabling Digital Wallet consumption tracking inside Salesforce Demo Orgs (SDOs) for the first time. Previously, Digital Wallet was only available in active customer orgs. This kit deploys Digital Wallet into an SDO with pre-built reports, dashboards, and Data Lake Objects (DLOs) showing consumption for Data 360 and Agentforce. Primarily relevant for pre-sales demos and partner enablement, but the underlying DLO/reporting architecture reveals how Salesforce meters consumption internally.

## Key Takeaways

### What Digital Wallet Is
- Consumption tracking and billing insight tool for consumption-based products (Data 360, Agentforce)
- Shows: consumption by agent, by usage type, by Data 360 resource, by tag
- Built on top of Data 360 DLOs — the consumption data is stored as Data Lake Objects in Data Cloud

### Underlying Data Architecture
- **TenantBillingUsageEvent** Data Stream: raw billing events ingested into Data Cloud
- **TenantEnrichedUsageEvent** DLO: enriched, queryable consumption data — the source for all reports and dashboards
- DLO fields include "consumption tags" — dimensions for slicing by: agent name, action type, feature, environment
- Sync cadence: 12 hours standard; manual refresh via TenantBillingUsageEvent Data Stream for faster updates
- Custom reports can be built on the TenantEnrichedUsageEvent DLO directly in Report Builder

### Reports and Dashboards
- Out-of-box reports in "Consumption Insights by Tags" folder
- Dashboard: "Digital Wallet Consumption Insights by Tags" — filterable by time period
- Views: consumption by agent (granular Agentforce cost attribution), by Data 360 resource type, by usage type

### SDO Constraints
- Only available in new SDOs that have not previously enabled Data 360
- Traditional consumption card experience (billing summary UI) not available in SDO
- Data refresh delay: 12 hours (unless manually triggered)

### Setup Flow
1. Get new SDO via Partner Learning Camp
2. Enable Data 360 (Data Cloud Setup)
3. Enable Digital Wallet (Setup → Digital Wallet → Get Started)
4. Configure Data Space: add all DLOs to default Data Space without filters
5. Usage data appears in Reports, Dashboards, DLO Explorer as consumption events are generated

## Notable Quotes / Data Points
- Digital Wallet goes live in SDOs as of 2025-11-03 — recent addition to partner/pre-sales toolkit
- Consumption tags are the key dimension for cost attribution — architecture decision: define tag taxonomy at project start
- TenantEnrichedUsageEvent DLO enables custom reporting — organizations can build FinOps dashboards tailored to their own cost center structure

## Wiki Pages Updated
- [[data-360]] — Digital Wallet implementation detail: TenantBillingUsageEvent Data Stream + TenantEnrichedUsageEvent DLO as billing layer
- [[agentforce]] — Per-agent consumption tracking via Digital Wallet; consumption tags as attribution mechanism

## Gaps / Follow-up
- Tag taxonomy design: how are consumption tags defined? Are they configurable per deployment or fixed by Salesforce?
- Agentforce pricing model details: what unit is billed (conversation? action? token?)
- FinOps pattern: consumption tags suggest a cost attribution architecture — worth developing as a concept page
