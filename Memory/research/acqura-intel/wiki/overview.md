# Acqura Intel — Competitive Landscape Overview

> Evolving synthesis. Updated when new sources meaningfully shift the picture.
> Last updated: 2026-04-22 (11 sources ingested)

---

## Current Thesis

The paid media measurement stack is structurally broken at multiple layers — and the market knows it. GA4 can't track impressions, caps lookback at 90 days, and loses conversions to iOS privacy restrictions. The Meta Pixel alone now captures only 50–65% of actual conversions (third-party cookies fully deprecated in Chrome 2025). Point solutions are patching individual gaps: CAPI fixes the tracking layer; MTA + MMM + incrementality triangulation fixes the attribution layer; growth OS platforms fix the strategy layer. But no single tool closes the full loop from data infrastructure to growth decision.

**Acqura's opportunity sits above the measurement layer, but below it is a prerequisite.** Broken tracking (Pixel-only, low EMQ, missing fbclid capture) is the default state for SMB clients — it must be remediated before GTI can generate reliable cross-channel recommendations. The practical entry point: a tracking health audit (check EMQ scores, CAPI coverage, fbclid capture rate) establishes trust and creates a billable setup phase before intelligence work begins.

---

## Landscape Clusters

- **Attribution & measurement** — 2 sources (Apr 20). GA4 limitations well-mapped. Triangulation framework (MTA + MMM + incrementality) established as current best practice. [[ruler-analytics]] identified as competitor analogue.
- **Meta tracking infrastructure** — 6 sources (Apr 22). CAPI coverage is now comprehensive: why it exists, how to implement, how to troubleshoot, 2026 state. [[meta-conversions-api]] is the synthesized concept page.
- **Meta data access tools** — 2 sources (Apr 22). [[meta-ad-library]] (competitor research via API — EU/political only; US requires scraping); [[meta-content-library-data-dictionary]] (academic research tool, low ad relevance).
- **D2C operational challenges** — 1 source (Apr 22). [[d2c-rto]] — India-specific Return to Origin problem; relevant only for Indian D2C clients.
- **Paid media platforms** — 0 deep sources. [[meta-platform]] entity created (from CAPI sources). Google, TikTok, programmatic not yet covered.
- **Growth OS / Revenue Intelligence** — 0 sources. Highest priority gap.
- **Audience & intent data** — 0 sources.

---

## Key Open Questions

- What does the Growth OS / Revenue Intelligence category look like today — who owns it, what's missing?
- Where does GTI fit relative to MTA + MMM + incrementality — as an integrator, a layer above, or something orthogonal?
- If Meta's Advantage+ AI consumes CAPI signal directly and optimizes campaigns autonomously, what incremental value does an external intelligence layer (Acqura GTI) add for pure Meta campaigns? Answer must be: cross-channel (Meta + Google + programmatic), not just within Meta.
- At what EMQ threshold does Advantage+ perform well enough that human or GTI optimization is unnecessary?
- How widespread is RTO outside India — does this affect Acqura's SEA or Middle East client positioning?
- Should Acqura build a tracking audit product as an entry-point offering, or treat it as a prerequisite check before onboarding?

---

## Gaps in the Wiki

- No sources on Growth OS / Revenue Intelligence competitors — highest priority
- No sources on Northbeam, Triple Whale — named in early sources, not yet ingested
- No sources on Google Ads, TikTok Ads, programmatic — only Meta deeply covered
- No sources on ABM, intent data, CDPs
- No sources on GCLID / Google Click ID (Google's equivalent to fbclid)
- Ruler Analytics pricing, scale, and full product surface unknown
- MMM at SMB scale — practical viability unclear
- Meta Ad Library API: EU-only limitation means US competitive intelligence via API is not viable — no solution sourced yet

---

## Acqura Implications

- **Tracking health audit as entry point**: Before GTI work begins, run EMQ check + CAPI coverage audit for every client. Low EMQ (below 6) = wasted ad spend right now; fixing it is a quick win with measurable ROI. Establishes Acqura as technically credible before selling intelligence.
- **CAPI is table stakes, not differentiator**: Don't compete here. Refer clients to Shopify/WooCommerce native integration (free) or Weld (Reverse-ETL for omni-channel). Acqura's value is above this layer.
- **Broken tracking = distorted data = wrong GTI inputs**: RTO-adjusted ROAS (for Indian D2C), EMQ-normalized attribution, fbclid-to-CRM pipeline — Acqura should surface these data quality gaps in its diagnostic output.
- **Clients arrive with a measurement spectrum**: broken UTM (no CAPI, no fbclid) → partial (GA4 only, no CAPI) → functional (CAPI live, EMQ 6+) → sophisticated (CAPI + fbclid + MTA + MMM). Acqura's GTI needs to work across this spectrum, diagnosing where each client is and what's needed before intelligence can be trusted.
- **First-party data is the moat**: CAPI, fbclid, email-at-checkout — the clients who capture this data with consent are future-proofed as privacy regulations tighten. Acqura should coach clients toward first-party data collection as a growth operating principle, not just a compliance measure.
- **The measurement problem is being commoditised** (Google Meridian, Meta Robyn are open-source MMM). The intelligence-above-measurement layer is not.

---

> Last updated: 2026-04-22 (11 sources ingested: 2 attribution, 6 CAPI/Meta tracking, 2 Meta data access, 1 D2C/RTO)
