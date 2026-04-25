---
title: Campaign Naming Conventions — The Key to Cleaner and Reliable Reporting
type: source
format: article
url: https://supermetrics.com/blog/campaign-naming-conventions
author: Supermetrics
date_published: 2025-01-01
date_ingested: 2026-04-25
tags: [campaign-naming, key-value, positional, taxonomy, data-transformation, reporting]
---

# Campaign Naming Conventions — The Key to Cleaner and Reliable Reporting

## Summary

Supermetrics' guide provides the clearest explanation of the two naming schema architectures — **delimiter-based (positional)** vs. **key-value pair** — including their trade-offs and failure modes. Uniquely, it covers the downstream data transformation step: using "split text to columns" (Excel/Sheets) or SQL to extract campaign name components into analytics fields for granular reporting. **Vendor note: Supermetrics is a data connector platform that moves ad data into BI tools — their value is in transforming structured campaign names into filterable analytics dimensions.**

## Key Takeaways

- **Two naming architectures — and why the trade-off matters:**
  - **Delimiter-based (positional):** `US_FA_TOFU_NewBrandImage_Aug2024`. Simple and readable, but order is critical — a missing field shifts every subsequent field, breaking all parsing. Requires placeholder (`NA`) for empty fields. Cannot add fields except at the end.
  - **Key-value pair:** `country*US_ds*FA_funnel*TOFU_theme*NewBrandImage_start*Aug2024`. Order-independent; missing fields don't shift others; new fields can be inserted anywhere without updating existing names. More complex to parse. **Preferred for large-scale or evolving campaigns.**
- **Data transformation is where naming pays off:** Once campaign names are structured, "split text to columns" in spreadsheets, SQL in data warehouses, or Supermetrics' custom fields can extract each component into its own analytics dimension — enabling filtering by product, country, funnel stage, or creative theme across all channels in a single dashboard view.
- Campaign hierarchy maps to account → campaign → ad group/set → ad level. Naming should be consistent across levels but the specificity of information increases with depth.
- **CamelCase vs. lowercase:** The author uses CamelCase (instead of hyphens or underscores) to avoid data parsing issues — an alternative convention worth noting, though most practitioner guides recommend lowercase with underscores/hyphens for URL-safety.
- UTM parameters should mirror the campaign naming structure for end-to-end tracking. `utm_campaign` maps to campaign name or ad group name depending on analytics granularity.

## Notable Quotes / Data Points

> "The key-value pair method is better when dealing with many fields, frequent changes, and potential missing data."

> "Without a naming convention, this level of analysis would require significant manual effort; some data might be irretrievable."

## Wiki Pages Updated

- [[campaign-naming-conventions]] — positional vs. key-value trade-off analysis; data transformation layer (SQL, split-text, BI tools); failure modes of positional naming
- [[supermetrics]] — entity page created; data connector + transformation platform; relevant to Acqura Tier 1 clients who use Supermetrics for reporting
- [[utm-tracking]] — UTM granularity decision: mirror campaign name vs. ad group name depending on analytics depth needed

## Gaps / Follow-up

- The key-value pair separator used here (`*`) differs from other sources (`:`). Acqura's TIP taxonomy needs a single defined separator and must document it.
- No guidance on how to handle retroactive migration of legacy campaigns to a new naming scheme — a practical problem for every Tier 1 client onboarding.
