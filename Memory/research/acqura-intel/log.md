# Acqura Intel Wiki — Activity Log

> Append-only. Never edit or delete past entries.
> Grep all entries: `grep "^## \[" Memory/research/acqura-intel/log.md`

---

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
