---
title: How to Implement Meta CAPI — Step-by-Step Guide 2026 (Weld)
type: source
format: article
url: raw/How to Implement Facebook  Meta Conversions API (CAPI) Step-By-Step Guide 2026.md
author: Weld
date_published: 2026-01-01
date_ingested: 2026-04-22
tags: [meta, capi, weld, reverse-etl, 2026, omnichannel, offline-conversions, b2b, deduplication]
---

# How to Implement Meta CAPI — Step-by-Step Guide 2026 (Weld)

## Summary
The most current and comprehensive CAPI guide (2026 perspective). Written by Weld, a Reverse-ETL platform with native CAPI integration. Establishes CAPI as essential infrastructure in 2026 with specific context: Chrome's third-party cookie deprecation (2025), Meta's legacy Offline Conversions API sunset (May 2025), and Datasets as the new central architecture layer. Covers use cases for omni-channel retail, B2B SaaS lead funnels, and app+web businesses. Includes detailed parameter reference, deduplication methods, monitoring, and how to prove CAPI lift.

## Key Takeaways

### 2026 Context — Why CAPI Is Now Mandatory
- Chrome completed third-party cookie phaseout in 2025 — server-side is now the primary reliable signal source
- **Legacy Offline Conversions API discontinued May 2025** — all offline/physical store events must now go through CAPI (`action_source: physical_store`; event_time can go up to 62 days back vs 7 days for web events)
- Meta's modern architecture centers on **Datasets** — unified pipeline for web, app, offline, and messaging events; CAPI is the central ingestion layer
- Advantage+ and AI campaigns depend on complete CAPI signal quality; incomplete data = poor optimization and wasted budget
- **Pixel-only: 50–65% conversion capture; Pixel + CAPI: 95%+ capture**

### Use Cases
1. **Omni-channel retailer (online + physical stores)**: CAPI sends missing online events + in-store purchases via `action_source: physical_store` — gives Meta full picture for optimization
2. **B2B SaaS lead funnel**: Pixel only sees initial form fill; CAPI sends downstream events (demo booked, qualified lead, closed deal) from CRM via [Conversion Leads Integration](https://developers.facebook.com/docs/marketing-api/conversions-api/conversion-leads-integration) — trains Meta to optimize for leads that convert, not just form fills
3. **App + web business**: CAPI now supports app events via same unified endpoint as web events

### Deduplication Methods
- **Method 1 (recommended)**: `event_id` + `event_name` matching — same combination on Pixel and CAPI within 48 hours = deduplicated; pattern: `Purchase:order_123` (string format)
- **Method 2 (fallback)**: `fbp` (browser cookie) + `external_id` — useful when Pixel and server don't share a common transaction ID; only deduplicates browser events arriving before server events

### Proving CAPI Lift
- **"Additional conversions reported"** metric in Events Manager — direct measurement of CAPI lift vs Pixel-only
- Pre/post KPIs: total conversions (+20–40% typical), EMQ score (upward trend), cost per conversion (decrease), deduplication rate (consistent activity)
- Conversion Lift Studies: rigorous A/B measurement of incremental server event impact on campaign performance

### Weld's Positioning
Weld is a Reverse-ETL platform (ELT + Reverse-ETL over BigQuery/Snowflake). Their CAPI use case: build SQL data model over CRM/POS/e-commerce data → sync to Meta CAPI on a schedule (e.g., every 30 minutes). Targeted at omni-channel brands too complex for Shopify's native integration.

## Notable Quotes / Data Points
> "We've observed that companies relying only on client-side tracking see just 50-65% of conversions inside Meta Ads Manager. After implementing CAPI, that number jumps to 95%+."
> "Meta now considers [CAPI] a baseline requirement for serious advertisers."
> "If you were previously using Meta's Offline Conversions API to upload store sales or other offline events, you must now use the Conversions API instead. CAPI handles offline events natively."

## Wiki Pages Updated
- [[meta-platform]] — 2026 state, Datasets architecture, offline API sunset
- [[meta-conversions-api]] — 95%+ stat, use cases, deduplication methods, Conversion Lift Studies
- [[first-party-mta]] — B2B lead funnel use case shows CAPI as enabler of downstream funnel events for MTA

## Gaps / Follow-up
- Weld is a potential partner for Acqura clients who need CAPI set up before GTI work can begin — evaluate as referral option
- Dataset Quality API (programmatic monitoring of event quality at scale) — worth noting for enterprise clients
