---
name: Marketing Mix Modelling (MMM)
type: concept
category: strategy
tags: [mmm, attribution, bayesian, shapley, budget-optimisation, upper-funnel, econometrics]
sources: 1
last_updated: 2026-04-20
---

# Marketing Mix Modelling (MMM)

## Definition

Marketing Mix Modelling (MMM) is an econometric / statistical approach that estimates the contribution of each marketing channel — including non-click interactions like impressions — to business outcomes (revenue, conversions). Modern implementations use Bayesian statistics and Shapley value to distribute credit across channels while accounting for external factors (seasonality, macroeconomics, competitor activity). Unlike MTA, MMM operates at the aggregate level, not individual user level, making it privacy-safe and impression-aware.

## Why It Matters for Acqura

MMM is the only method that can quantify the value of upper-funnel marketing (brand, display, awareness) that generates no trackable clicks. It's also the primary tool for budget optimisation — generating diminishing return curves that show where additional spend stops producing proportional revenue. Understanding MMM is critical for Acqura because: (1) clients investing in upper-funnel will need it; (2) budget optimisation outputs are exactly the kind of actionable intelligence a Growth OS should surface.

## How It Works

- Ingests historical data: ad spend by channel, revenue/conversion outcomes, external variables
- Statistical model decomposes revenue into base (organic) and incremental (paid) components
- Shapley value distributes marginal contribution fairly across channels, including impression-based ones
- Bayesian inference handles uncertainty and updates as new data arrives
- Output: diminishing return curves per channel — shows the revenue headroom available at current spend levels
- Output: budget allocation recommendations — how to shift spend to maximise return

## Key Practitioners / Platforms

- [[ruler-analytics]] — MMM embedded alongside MTA in one platform
- Nielsen Marketing Mix — traditional enterprise MMM
- Analytic Partners — enterprise MMM and scenario planning
- Google Meridian — Google's open-source MMM framework (Bayesian)
- Meta Robyn — Meta's open-source MMM framework

## Acqura's Angle

MMM outputs (diminishing returns, budget allocation) are high-value intelligence that currently requires significant data and analytical overhead to produce. If Acqura's GTI framework could simplify access to MMM-style insights — or integrate with tools that produce them — it would give clients the strategic layer they currently lack. The Acqura question: is MMM an input to Growth OS decision-making, or something Acqura helps clients operationalise?

## Contradictions / Open Questions

- MMM traditionally requires 2+ years of historical data and significant ad spend to be statistically meaningful — accessible to SMBs?
- Google Meridian and Meta Robyn are open-source — does this commoditise MMM and remove vendor value?
- How frequently can MMM models be updated — weekly, monthly? Real-time MMM is an open research problem.
- Shapley value is computationally expensive at scale — practical limitations?

## Sources

- [[ruler-facebook-ads-ga4-2026]] — introduced MMM in context of triangulation framework; Bayesian/Shapley implementation, diminishing returns curves
