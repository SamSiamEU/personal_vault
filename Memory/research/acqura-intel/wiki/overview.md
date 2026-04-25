# Acqura Intel — Competitive Landscape Overview

> Evolving synthesis. Updated when new sources meaningfully shift the picture.
> Last updated: 2026-04-22 (11 sources ingested)

---

## Current Thesis

The paid media measurement stack is structurally broken at multiple layers — and the market knows it. GA4 can't track impressions, caps lookback at 90 days, and loses conversions to iOS privacy restrictions. The Meta Pixel alone now captures only 50–65% of actual conversions (third-party cookies fully deprecated in Chrome 2025). Point solutions are patching individual gaps: CAPI fixes the tracking layer; MTA + MMM + incrementality triangulation fixes the attribution layer; growth OS platforms fix the strategy layer. But no single tool closes the full loop from data infrastructure to growth decision.

**Acqura's opportunity sits above the measurement layer, but below it is a prerequisite.** Broken tracking (Pixel-only, low EMQ, missing fbclid capture) is the default state for SMB clients — it must be remediated before GTI can generate reliable cross-channel recommendations. The practical entry point: a tracking health audit (check EMQ scores, CAPI coverage, fbclid capture rate) establishes trust and creates a billable setup phase before intelligence work begins.

Beyond tracking infrastructure, most clients have a deeper strategic failure: **they optimise entirely for "Do" intent audiences** (strong purchase intent) while ignoring "See" (awareness), "Think" (consideration), and "Care" (retention) audiences. The result is expensive competition over a thin slice of the market, while the much larger qualified audience pool is unreached. Acqura's GTI should diagnose this intent distribution gap and structure recommendations accordingly — each recommendation tagged to an intent cluster with cluster-appropriate success metrics. (See [[see-think-do-care]].)

---

## Landscape Clusters

- **Attribution & measurement** — 2 sources (Apr 20). GA4 limitations well-mapped. Triangulation framework (MTA + MMM + incrementality) established as current best practice. [[ruler-analytics]] identified as competitor analogue.
- **Meta tracking infrastructure** — 6 sources (Apr 22). CAPI coverage is now comprehensive: why it exists, how to implement, how to troubleshoot, 2026 state. [[meta-conversions-api]] is the synthesized concept page.
- **Meta data access tools** — 2 sources (Apr 22). [[meta-ad-library]] (competitor research via API — EU/political only; US requires scraping); [[meta-content-library-data-dictionary]] (academic research tool, low ad relevance).
- **Analytics strategy frameworks** — 2 sources (Apr 24, Avinash Kaushik). [[see-think-do-care]] — audience intent cluster framework; 97% of marketing spend concentrated on Do intent; LAQA concept; per-cluster metrics. [[analytics-maturity-model]] — three-phase maturity model (Data Capture → Reporting → Analysis); IABI output framework (Insights → Actions → Business Impact); 10/90 rule (invest $90 in analysts, $10 in tools). Both directly inform how Acqura's GTI should be positioned and structured.
- **D2C operational challenges** — 2 sources (Apr 22 + Apr 24). [[d2c-rto]] significantly deepened: inflated dashboard problem (COD dashboards overstate revenue), reconciliation complexity, AI voice agents for COD management, COD-to-prepaid conversion as strategic lever.
- **Campaign taxonomy & data governance** — 6 sources (Apr 25). [[campaign-naming-conventions]] is the synthesised concept page. Establishes the 4-layer naming hierarchy (asset → ad → ad set → campaign), the stable creative ID as the critical join key for cross-channel attribution, and the positional vs. key-value schema trade-off. [[improvado]] and [[supermetrics]] identified as competitive platforms/integration points. Key Acqura implication: Campaign ID governance (Tier 1 core deliverable) is being commoditised by AI-powered governance tools — Acqura's defence is the intelligence layer above the clean taxonomy.
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
- **COD dashboard distortion** (Indian D2C clients): COD orders inflate conversion counts; only ~65% of "orders" become real revenue. Acqura's diagnostic should include a COD distortion check — RTO-adjusted ROAS by campaign and audience segment — before any GTI recommendation is made. (See [[d2c-rto]].)
- **Clients arrive with a measurement spectrum**: broken UTM (no CAPI, no fbclid) → partial (GA4 only, no CAPI) → functional (CAPI live, EMQ 6+) → sophisticated (CAPI + fbclid + MTA + MMM). Acqura's GTI needs to work across this spectrum, diagnosing where each client is and what's needed before intelligence can be trusted.
- **Clients also arrive on an analytics maturity spectrum**: Phase 1 (data capture only) → Phase 2 (reporting) → Phase 3 (analysis/IABI). GTI output format should match client maturity: audit-first for Phase 1, insight reports for Phase 2, full IABI recommendations for Phase 3. (See [[analytics-maturity-model]].)
- **GTI output should be IABI-structured**: Insight (what the data says and why) → Action (specific recommendation) → Business Impact (quantified). This is the standard clients never receive — it is Acqura's differentiation vs. dashboards and reports.
- **Most clients are Do-intent only**: all measurement and optimisation is concentrated on conversion-stage audiences. Acqura's GTI should diagnose the intent gap (what % of spend is See vs. Think vs. Do vs. Care) and recommend rebalancing where economics support it. (See [[see-think-do-care]].)
- **First-party data is the moat**: CAPI, fbclid, email-at-checkout — the clients who capture this data with consent are future-proofed as privacy regulations tighten. Acqura should coach clients toward first-party data collection as a growth operating principle, not just a compliance measure.
- **The measurement problem is being commoditised** (Google Meridian, Meta Robyn are open-source MMM). The intelligence-above-measurement layer is not. Acqura sells the 90 in the 10/90 rule — the analyst brain, not the tool.
- **Campaign ID governance is the Tier 1 foundation — but the setup work is being automated away.** Improvado's AI governance (500+ source connectors, real-time name validation, platform sync-back) and Trackingplan's UTM monitoring do manually what Acqura's Tier 1 governance delivers as a consulting service. The defensible value is: (1) designing the taxonomy itself (requires strategic judgment, not just tooling); (2) the creative ID as join key for RTO-adjusted ROAS at creative level (no governance tool does this for Indian D2C); and (3) the GTI intelligence built on top of the clean data. Governance setup alone is not a defensible product.
- **Creative ID is the GTI join key for RTO-adjusted ROAS.** For Acqura's killer Tier 1 feature (RTO-adjusted ROAS by campaign and creative segment), the stable creative ID in `utm_content` is what links ad platform spend → GA4 sessions → order management system returns. Without it, RTO-adjusted ROAS is only calculable at campaign level — not at the creative/audience level where the insight is actionable.
- **Supermetrics + BigQuery + structured naming = a lightweight DIY Tier 1 stack.** Clients who already run Supermetrics feeding a BigQuery warehouse with a naming convention in place have the data infrastructure layer solved. Acqura's entry point for these clients is not setup — it is the GTI intelligence layer above the data. Adjust Tier 1 onboarding accordingly.

---

> Last updated: 2026-04-25 (20 sources ingested: 2 attribution, 6 CAPI/Meta tracking, 2 Meta data access, 1 D2C/RTO, 2 analytics strategy, 1 D2C/COD, 6 campaign naming conventions)
