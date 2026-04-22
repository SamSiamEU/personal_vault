# Acqura Intel Wiki — Activity Log

> Append-only. Never edit or delete past entries.
> Grep all entries: `grep "^## \[" Memory/research/acqura-intel/log.md`

---

## [2026-04-22] ingest | Batch Ingest — 9 new raw files (Meta CAPI cluster + D2C RTO)

**Source type**: External references (practitioner guides, Meta official docs, D2C operations article)
**New files**: 9 files added to raw/ since last session

**Dominant theme (7 of 9 files)**: Meta Conversions API / server-side tracking — covering foundational concepts, step-by-step setup, 2026 state-of-the-art, troubleshooting, fbclid capture, Ad Library API, and Content Library data dictionary

**Files processed**:
- `A Comprehensive Guide to Server-Side Tracking and the Meta Conversion API.md` — conceptual intro, Pixel vs CAPI
- `Meta Conversions API Setup Guide.md` — AdAmigo setup guide with performance benchmarks
- `How to Implement Facebook Meta Conversions API (CAPI) Step-By-Step Guide 2026.md` — Weld, 2026 definitive guide; 50-65% → 95%+ capture stat; Offline API sunset
- `Meta Conversions API Complete Setup & Optimization Guide (2026).md` — AdsUploader; 4 setup methods, EMQ scoring, 15 troubleshooting issues
- `How to Capture the Meta Click ID (fbclid) With Your Funnel.md` — Heyflow, fbclid mechanism and capture
- `How to use the Meta ad library API to scrape ad data?.md` — Swipekit; Ad Library API (EU-only limitation)
- `Meta Content Library and API Data Dictionary.md` — Meta official data dictionary for research access
- `How to use Facebook Graph API and extract data using Python!.md` — dated (2017, v2.7) tutorial; low relevance
- `Reducing RTO in D2C Businesses Challenges & Solutions.md` — India D2C; COD dependency; BNPL; AI fraud scoring

**Source pages created (9)**:
- [[server-side-tracking-meta-capi-intro]]
- [[meta-capi-setup-guide-adamigo]]
- [[meta-capi-implementation-guide-2026-weld]]
- [[meta-capi-complete-guide-adsuploader]]
- [[fbclid-capture-heyflow]]
- [[meta-ad-library-api-swipekit]]
- [[meta-content-library-data-dictionary]]
- [[facebook-graph-api-python-basics]]
- [[d2c-rto-reduction-bnpl]]

**Entity pages created (1)**:
- [[meta-platform]] — Meta (Facebook/Instagram) advertising ecosystem; Pixel, CAPI, EMQ, Ad Library, Advantage+; dual tracking architecture; 2026 state

**Concept pages created (3)**:
- [[meta-conversions-api]] — Major concept; CAPI mechanics, dual tracking, EMQ scoring, 4 setup methods, benchmarks (95%+ capture), Acqura implications
- [[meta-ad-library]] — Ad Library API for competitor research; EU-only API limitation; scraping tools for US
- [[d2c-rto]] — Return to Origin in Indian D2C; COD dependency; BNPL; RTO-adjusted ROAS

**Overview.md**: significantly updated — new thesis section on CAPI as prerequisite, tracking health audit as Acqura entry point, first-party data as moat; new landscape cluster (Meta tracking infrastructure); updated open questions and Acqura implications

**Synthesis note**: The 9 new sources establish a comprehensive picture of the Meta tracking infrastructure layer. The key Acqura implication: broken CAPI (Pixel-only = 50-65% conversion capture) is the default state for SMB clients — a tracking health audit (EMQ check, CAPI coverage, fbclid capture) is the natural Acqura entry point before GTI delivers reliable recommendations. CAPI itself is table stakes infrastructure, not a differentiator; Acqura's value is the intelligence layer above it. The B2B lead funnel use case (CAPI sending downstream CRM events) is directly analogous to Acqura's first-party MTA positioning.

## [2026-04-20] ingest | How to Track Facebook Ads in Google Analytics: Complete 2026 Tutorial

- Format: article | Author: Ruler Analytics | Source file: `raw/How to Track Facebook Ads in Google Analytics Complete 2026 Tutorial.md`
- Pages created: `sources/ruler-facebook-ads-ga4-2026`, `entities/ruler-analytics`, `concepts/marketing-measurement-triangulation`, `concepts/first-party-mta`, `concepts/marketing-mix-modelling`, `concepts/incrementality-testing`, `concepts/impression-attribution`
- Pages updated: `concepts/utm-tracking` (Facebook best practices, triangulation link), `wiki/overview.md` (thesis updated, Acqura implications deepened), `index.md`
- Synthesis: GA4 has three structural limits for Facebook tracking (no individual users, 90-day lookback, no impressions). iOS 14 is structural — 40% conversion loss is permanent. The triangulation framework (MTA + MMM + incrementality) maps the measurement sophistication ceiling. Ruler Analytics is a direct Acqura analogue — measurement layer, not intelligence layer. Acqura's position: above the measurement, not inside it.

---

## [2026-04-20] ingest | UTM ID: Why You Must Include It in Your Ad Tracking

- Format: article | Author: OWOX | Source file: `raw/UTM ID Why You Must Include It in Your Ad Tracking.md`
- Pages created: `sources/owox-utm-id-ad-tracking`, `entities/owox`, `concepts/utm-tracking`, `concepts/ga4-cost-data-import`
- Pages updated: `wiki/overview.md` (first thesis seed, open questions, gaps), `index.md`
- Synthesis: utm_id is the commonly-missed fourth required UTM tag for GA4 cost data import. Silent failure (0% match rate) is the key trap. OWOX is a point solution in a fragmented measurement market. Core Acqura implication: clients arrive with broken data plumbing; the full-stack Growth OS category is underdeveloped.

---

## [2026-04-20] init | Wiki initialized

- Structure created: CLAUDE.md, index.md, log.md, wiki/ skeleton
- Domain: competitive landscape for paid media systems and growth OS platforms
- Scope: entities (platforms, tools, competitors), concepts (strategies, frameworks, metrics), sources, analyses
- Status: ready for first ingest
