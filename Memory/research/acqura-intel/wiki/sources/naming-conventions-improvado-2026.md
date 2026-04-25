---
title: Campaign Naming Conventions — A Complete Guide to Best Practices (2026)
type: source
format: article
url: https://improvado.io/blog/marketing-campaign-naming-conventions
author: Improvado
date_published: 2026-01-01
date_ingested: 2026-04-25
tags: [campaign-naming, taxonomy, governance, salesforce, ai-governance, data-quality]
---

# Campaign Naming Conventions — A Complete Guide to Best Practices (2026)

## Summary

Improvado's guide provides the clearest hierarchical framework for campaign naming across three levels (campaign, ad set, ad creative) with concrete naming examples for Google Ads, Facebook Ads, and — notably — **Salesforce Campaigns**. The final section introduces AI-powered Marketing Data Governance that auto-validates and corrects campaign names across 500+ ad sources in real time. **Vendor note: Improvado is a marketing analytics and data governance platform — their AI governance product is a direct competitor to Acqura's manual Campaign ID governance service in Tier 1.**

## Key Takeaways

- **Hierarchical naming framework across three levels:** Campaign level (objective, audience, platform, date, theme) → Ad Set level (audience details, bid strategy, placement, creative type) → Ad Creative level (creative ID, version, message, CTA, format specs).
- **Google Ads example:** `SEARCH_LeadGen_ProductX_US_Q32025` at campaign; `AG_ProductX_KeywordGroup_CompetitorBrand_BMM` at ad group; `AD_ProductX_Offer1_HeadlineA_DescV2_CTA_LearnMore` at ad.
- **Facebook Ads example:** `FB_CONVERSION_Shoes_SummerSale_US_AUG25` at campaign; `AS_Retarget_WebsiteVisitors_Last30Days_ValueAudience_BID_CPA` at ad set.
- **Salesforce Campaigns example:** `SF_WEBINAR_LeadGen_Q2_2026_ProductDemo` — naming conventions extend to CRM campaign tracking, not just ad platforms. Cross-platform naming consistency (SF ↔ Meta ↔ Google) is a multi-touch attribution requirement.
- **Privacy note:** Campaign names appear in UTM parameters visible in browser URLs — avoid encoding actual audience names, budget figures, or sensitive internal codes in campaign names that end up in UTM strings.
- **AI-powered governance (Improvado "Marketing Data Governance"):** Auto-validates campaign names across 500+ sources, flags discrepancies in real time, AI-suggests corrections, syncs back to platforms (Google Ads, Meta, TikTok). Unifies data from 500+ ad sources with harmonised metrics.
- Five best practices: consistency above all, clear delimiters (underscores preferred), no special characters, UTM alignment (utm_campaign mirrors campaign name), centralised documentation.

## Notable Quotes / Data Points

> "The single most critical aspect of any naming convention is consistency."

- Case study: Improvado acts as "default QA mechanism for Eicoff clients' media campaigns" (SVP Innovation, Eicoff).
- The pitfall table is the most useful diagnostic: changing names post-launch, inconsistent use across channels, over-complication, neglecting to update naming rules, failing to pilot first.

## Wiki Pages Updated

- [[campaign-naming-conventions]] — hierarchical three-level framework; Salesforce Campaign naming; AI governance threat; pitfall table
- [[improvado]] — entity page created; AI-powered marketing data governance; 500+ ad source connectors; competitive position relative to Acqura Tier 1
- [[utm-tracking]] — privacy note: UTM parameters are visible in browser URLs; encode with coded identifiers rather than raw audience names

## Gaps / Follow-up

- Improvado's AI governance pricing is unknown — if it's under €500/month it undercuts Acqura's Tier 1 campaign governance component significantly.
- The Salesforce Campaign naming example is worth expanding — how does SFMC Campaign naming integrate with paid media UTMs for closed-loop attribution? This is directly relevant to Acqura Tier 2/3.
