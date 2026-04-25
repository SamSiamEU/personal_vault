---
name: Supermetrics
type: entity
category: platform
tags: [data-connector, campaign-naming, reporting, data-transformation, bi-tools]
sources: 1
last_updated: 2026-04-25
---

# Supermetrics

## What It Is

Supermetrics is a data connector and transformation platform that moves ad data from 100+ ad sources (Meta, Google, TikTok, LinkedIn, Bing, etc.) into reporting destinations (Google Sheets, Looker Studio, BigQuery, Power BI, Snowflake). Its primary value is bridging ad platform exports to BI tools. It includes data transformation capabilities that extract structured analytics from campaign names — splitting name components into individual dimensions for granular cross-channel reporting.

## Relevance to Acqura

**Tool used by Acqura's Tier 1 clients** more than a competitor. Indian D2C brands using MoEngage or Braze for lifecycle marketing often use Supermetrics to pull ad data into Sheets or Looker Studio. Acqura's Campaign ID governance work creates structured campaign names that Supermetrics can then parse and transform into clean analytics — making Supermetrics an integration point, not a competitor. However, if a client already uses Supermetrics with a campaign naming convention in place, Acqura's governance setup value is compressed.

## Key Capabilities

- 100+ ad platform connectors into Google Sheets, BigQuery, Looker Studio, Power BI, Snowflake
- Data transformation: "split text to columns" on campaign names to extract taxonomy dimensions
- Custom fields in Supermetrics Hub: extract country, funnel stage, creative type from campaign name components
- SQL-compatible export to data warehouses for joining ad data to backend conversion data
- UTM parameter handling: transforms UTM values into reporting dimensions

## Pricing / Business Model

[unknown] — tiered SaaS model; individual plan, business, and enterprise. Likely €200–800/month for mid-market depending on connector count and destination.

## Strengths

- Widely used by performance marketing agencies and in-house teams
- If campaign names are structured, Supermetrics extracts maximum analytical value automatically
- BigQuery integration directly relevant to Acqura's Tier 1 BigQuery stack

## Weaknesses / Gaps

- Purely a data movement and transformation layer — no intelligence, no recommendations
- Requires structured campaign names to extract meaningful dimensions — does not enforce naming compliance (unlike Improvado)
- No Indian D2C or COD-adjusted reporting capabilities

## Contradictions / Open Questions

- Supermetrics + structured campaign naming + BigQuery = a lightweight Acqura Tier 1 stack without the GTI intelligence layer. How should Acqura position against this DIY configuration?

## Sources

- [[naming-conventions-supermetrics]] — key-value vs. positional trade-off; data transformation layer; BI reporting from structured campaign names
