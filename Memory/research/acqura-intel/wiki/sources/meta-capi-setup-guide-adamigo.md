---
title: Meta Conversions API Setup Guide (AdAmigo)
type: source
format: article
url: raw/Meta Conversions API Setup Guide.md
author: AdAmigo.ai
date_published: 2025-01-01
date_ingested: 2026-04-22
tags: [meta, capi, setup, emq, deduplication, events-manager, adamigo]
---

# Meta Conversions API Setup Guide (AdAmigo)

## Summary
Step-by-step setup guide for Meta CAPI from AdAmigo.ai (Meta Business Technology Partner). Covers prerequisites, Events Manager configuration, dual tracking setup, testing with `test_event_code`, Event Match Quality monitoring, and deduplication. Includes real-world performance stats from named brands.

## Key Takeaways
- Prerequisites: HTTPS site, domain verified in Meta Business Suite, admin access to Ad Account + Page + Pixel + Product Catalogs
- Access token generated in Events Manager → must be rotated; system user tokens preferred for stability
- Setup flow: Data Sources → Add Events → Add new integration → Conversions API → Set up manually
- Dual tracking target: at least 75% server event coverage vs Pixel events; 70%+ deduplication overlap
- EMQ target: 6+ minimum; add customer parameters (email, phone, click IDs) to improve
- Test workflow: add `test_event_code` to payload → validate in Test Events tab → remove before production
- Key metric to prove lift: "Additional conversions reported" in Events Manager (direct CAPI lift vs Pixel-only)

## Notable Quotes / Data Points
> "Events shared using the Conversions API require specific data parameters. These parameters contribute to improving the quality of events used for ad delivery and may improve campaign performance." — Meta Business Help Center

**Performance benchmarks:**
- **20% boost in purchase conversions** for businesses using CAPI
- **67% increase in reported purchases** for Diptyque (luxury fragrance brand)
- **13% lower costs per result** + **19% more attributed purchase events** (Meta aggregate data)
- **30% increase in purchases** + **25% reduction in cost per purchase** — YOOX NET-A-PORTER
- **43% boost in purchase conversion rates** in 2 weeks + **$1.1M in sales** — Full Harbor Clothing
- **W for Woman** (India fashion brand): 80% custom audience match rate, 35% lower cost per purchase, 20% incremental revenue increase
- **Dundas Life** (Canadian insurance): improved EMQ, 60% lower cost per lead in 2 weeks
- **BoxyCharm**: 23% increase in customer retention, 30% boost in ROAS over 4 months

## Wiki Pages Updated
- [[meta-conversions-api]] — benchmarks added, setup steps referenced
- [[meta-platform]] — performance benchmark context

## Gaps / Follow-up
- AdAmigo positions itself as an AI optimization layer on top of CAPI — positioning it as a potential analogue or competitor to Acqura's GTI in the Meta-specific optimization space
- The "Additional conversions reported" metric is the key KPI to prove CAPI lift — useful for Acqura client reporting
