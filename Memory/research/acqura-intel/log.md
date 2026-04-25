# Acqura Intel Wiki — Activity Log

> Append-only. Never edit or delete past entries.
> Grep all entries: `grep "^## \[" Memory/research/acqura-intel/log.md`

---

## [2026-04-25] ingest | Batch Ingest — 6 new raw files (Campaign Naming Conventions cluster)

**Source type**: External references (vendor blog articles — Trackingplan, AdManage.ai, Improvado, Supermetrics, PPCHero/Brainlabs, AdAmigo.ai)
**Files processed**: 6 of 7 new raw files; 1 skipped (Monetate — personalisation CMS tool, campaign naming for on-site experiments, out of scope for paid media intelligence)

**Dominant theme**: Campaign naming conventions as data taxonomy — the structural framework underlying Acqura's Tier 1 TIP taxonomy and Campaign ID governance deliverable

**Files processed**:
- `A Practical Guide to Campaign Naming Conventions.md` — Trackingplan; master dictionary, URL builder, governance automation
- `Ad Creative Naming Conventions Guide (2026).md` — AdManage.ai; 4-layer model, stable creative ID, decision vs. context fields
- `Campaign Naming Conventions A Complete Guide to Best Practices 2026.md` — Improvado; 3-level hierarchy, Salesforce Campaign naming, AI governance
- `Campaign Naming Conventions The Key to Cleaner and Reliable Reporting.md` — Supermetrics; positional vs. key-value trade-off, BI transformation
- `The Complete Guide To PPC Naming Conventions.md` — PPCHero/Brainlabs; parameters/fields/anchors/separators vocabulary, agency structure
- `Ultimate Guide to Meta Ad Naming Conventions 2025.md` — AdAmigo.ai; Meta templates, version control, AI automation

**Source pages created (6)**:
- [[naming-conventions-trackingplan-2026]]
- [[naming-conventions-admanage-creative-2026]]
- [[naming-conventions-improvado-2026]]
- [[naming-conventions-supermetrics]]
- [[naming-conventions-ppchero-brainlabs]]
- [[naming-conventions-adamigo-meta-2025]]

**Concept pages created (1)**:
- [[campaign-naming-conventions]] — 4-layer hierarchy; stable creative ID as join key; positional vs. key-value schema; governance layer; Acqura TIP taxonomy implications; commoditisation risk

**Entity pages created (2)**:
- [[improvado]] — AI-powered marketing data governance; 500+ connectors; direct Tier 1 competitor for campaign naming automation
- [[supermetrics]] — data connector + transformation platform; relevant as existing infrastructure in Tier 1 client environments

**Concept pages updated (1)**:
- [[utm-tracking]] — added campaign naming alignment section; utm_content as creative ID carrier; key-value pair for UTMs; privacy note on URL-visible parameters; sources count 1→4

**Overview.md**: new landscape cluster added (campaign taxonomy & data governance); two new Acqura implications (governance commoditisation; creative ID as GTI join key for RTO-adjusted ROAS; Supermetrics+BigQuery as DIY Tier 1 stack); source count updated to 20

**Synthesis note**: The campaign naming cluster confirms the market pain (80% of analyst time on data cleaning without naming conventions) and validates Acqura's Tier 1 TIP taxonomy as a genuine service gap. The critical finding: AI-powered governance (Improvado, Trackingplan) is automating the naming compliance layer, compressing the consulting value of "setting up a naming convention." Acqura's defensible Tier 1 value is (1) taxonomy design judgment, (2) creative ID integration for RTO-adjusted ROAS, and (3) the GTI intelligence built on the clean data — not governance setup alone. Vendors filing these sources are all potential competitors for parts of Acqura's stack.

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

## [2026-04-24] ingest | Batch Ingest — 3 new raw files (analytics strategy + COD/D2C)

**Source type**: External references (Avinash Kaushik blog posts x2, Pharynx.ai vendor blog x1)
**Dennis's framing**: First two files = strategic view on how to structure marketing analytics and get data to tell a story. Third file = market intelligence on COD challenges in India, important for Acqura Growth OS approach.

**Files processed**:
- `See, Think, Do, Care Winning Combo Content +Marketing +Measurement!.md` — Kaushik STDC framework extension; LAQA; trifecta requirement; per-cluster metrics
- `The Complete Digital Analytics Ecosystem How To Win Big.md` — Kaushik analytics ecosystem model; 10/90 rule; IABI output framework; 3-phase maturity model
- `Why Can't D2C brands avoid COD? And how AI is fixing its biggest challenges.md` — Pharynx.ai; inflated dashboard problem; COD reconciliation complexity; AI voice agents; COD-to-prepaid conversion

**Source pages created (3)**:
- [[kaushik-see-think-do-care]]
- [[kaushik-digital-analytics-ecosystem]]
- [[pharynx-d2c-cod-ai-challenges]]

**Concept pages created (2)**:
- [[see-think-do-care]] — full STDC framework: 4 intent clusters, LAQA, trifecta, per-cluster metrics table, Acqura angle (intent gap diagnosis, GTI output tagged by cluster, LTV as Care metric)
- [[analytics-maturity-model]] — 3-phase maturity model, IABI output frame, 10/90 rule, client diagnostic application, GTI positioning as the 90

**Concept pages updated (2)**:
- [[marketing-measurement-triangulation]] — IABI output frame added; STDC intent-cluster measurement alignment; cross-links to new concepts; sources count 1→3
- [[d2c-rto]] — inflated dashboard problem (10,000 orders → 6,500 delivered); COD reconciliation complexity; traditional channel failures; AI voice agent approach; COD-to-prepaid conversion as strategic priority; sources count 1→2

**Overview.md**: updated — new thesis paragraph on Do-intent bias; analytics strategy cluster added to landscape; D2C cluster updated; Acqura implications expanded (COD distortion check, analytics maturity spectrum, IABI GTI output, intent gap diagnosis, 10/90 rule positioning)

**Synthesis note**: The Kaushik sources provide the strategic vocabulary for how Acqura should think about its GTI output: structured as IABI (not dashboards), tagged to intent cluster (not just conversion events), delivered to clients where they are on the maturity curve (Phase 1 gets an audit, Phase 3 gets full intelligence). The COD article deepens the data distortion picture — for Indian D2C clients, conversion metrics in ad platforms are fundamentally unreliable without RTO adjustment, and the inflated dashboard problem means clients are scaling against ghost revenue. Together: Acqura's diagnostic entry point should surface both tracking gaps (CAPI/EMQ) and economic distortions (RTO-adjusted ROAS, COD share of conversions) before GTI recommendations are made.
