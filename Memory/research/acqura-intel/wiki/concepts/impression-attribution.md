---
name: Impression Attribution
type: concept
category: strategy
tags: [impression, view-through, upper-funnel, attribution, brand, display, cookies]
sources: 1
last_updated: 2026-04-20
---

# Impression Attribution

## Definition

Impression attribution (also: view-through attribution) assigns conversion credit to ad impressions — instances where a user *saw* an ad but did not click it — that preceded a conversion. It captures the influence of upper-funnel advertising (brand awareness, display, video) that generates no direct clicks but may significantly influence downstream purchase decisions. Distinct from click-through attribution, which only credits touchpoints where a user actively clicked.

## Why It Matters for Acqura

Click-based attribution systematically undervalues upper-funnel investment. A brand campaign that influences 1,000 people to search directly for a product will receive zero credit in click-based systems — all credit goes to organic search. As budgets tighten and marketers are asked to justify every channel, impression attribution becomes essential for defending upper-funnel spend. Acqura's Growth OS needs to account for impression influence in its intelligence layer, or it will perpetuate the same undervaluation bias.

## How It Works

- **Platform-native (view-through):** Meta and other platforms offer a 24-hour view-through attribution window — if a user saw an ad and converted within 24 hours, the impression gets credit. Relies on third-party cookies; increasingly unreliable post-iOS 14.
- **MMM-based impression modelling:** Statistical modelling estimates impression contribution at the aggregate level using Bayesian/Shapley methods. Privacy-safe, doesn't require individual user tracking.
- **Traffic pattern analysis (Ruler approach):** Analyses traffic spikes and behaviour patterns correlated with impression campaigns to infer influence, even without direct click linkage.

## Platform Limitations

- **Meta:** 24-hour view-through window — insufficient for B2B (typical sales cycles: days to months). Cookie-dependent.
- **GA4:** No native impression attribution — completely blind to ad views. This is one of GA4's three structural limits for Facebook tracking.
- **Google Ads:** View-through conversion window configurable (1–30 days) but still click-centric by default.

## Key Practitioners / Platforms

- [[ruler-analytics]] — ML-based impression attribution using Bayesian/Shapley; not cookie-dependent
- [[marketing-mix-modelling]] — primary vehicle for impression attribution at aggregate level
- Meta Ads Manager — native view-through attribution (limited, cookie-dependent)

## Acqura's Angle

Impression attribution is where most marketers have the biggest blind spot. Upper-funnel spend is chronically undervalued because it can't be click-tracked — this leads to systematic over-investment in bottom-funnel (retargeting, branded search) and under-investment in awareness. Acqura's intelligence layer should surface this bias and help clients recalibrate budget allocation. This is a high-value, underserved insight category.

## Contradictions / Open Questions

- Is 24-hour view-through window (Meta) meaningful at all, or does it create more attribution inflation than insight?
- MMM-based impression attribution requires historical data and statistical overhead — what's the practical floor for usable insights?
- As third-party cookies disappear entirely, does platform-native view-through attribution become worthless?

## Sources

- [[ruler-facebook-ads-ga4-2026]] — introduced impression attribution as gap in GA4; ML-based Bayesian/Shapley approach via Ruler; 24-hour Meta window limitation
