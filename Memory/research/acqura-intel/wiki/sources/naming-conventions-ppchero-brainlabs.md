---
title: The Complete Guide to PPC Naming Conventions
type: source
format: article
url: https://ppchero.com/the-complete-guide-to-ppc-naming-conventions
author: PPCHero / Brainlabs
date_published: 2024-08-01
date_ingested: 2026-04-25
tags: [campaign-naming, ppc, taxonomy, agency, cross-channel, parameters, anchors]
---

# The Complete Guide to PPC Naming Conventions

## Summary

The most rigorous vocabulary source in the cluster. Written by a senior Brainlabs strategist, this guide defines the four structural components of any naming convention — **parameters, fields, separators, anchors** — and applies them to cross-channel campaigns (Google Search, Shopping, Display, Social, Amazon). The agency perspective is uniquely valuable: it addresses multi-client governance, the granularity trade-off (control vs. manageability), and the common failure modes of misleading data from naming inconsistency.

## Key Takeaways

- **Four structural components of a naming convention:**
  - **Parameter:** The label for a type of information (e.g., Country, Product, Match Type). Appears in the convention doc but NOT in the campaign name itself.
  - **Field:** The actual value assigned to a parameter (e.g., USA, Chairs, Exact). Appears in the campaign name.
  - **Separator:** Character used to divide fields (underscore, pipe). Must be singular and consistent — enables text-to-column splitting in Excel/SQL.
  - **Anchor:** A prefix added to a field to disambiguate when the same field value appears in multiple parameters (e.g., `B-Brand A` to distinguish Brand parameter from Product parameter when both might use "All"). Underused but critical for large accounts.
- **Naming structure for agencies:** `[Agency Parameters]_[Universal Parameters]_[Common Parameters]_[Unique Parameters]` — most-commonly-used parameters come first; platform-unique parameters at the end (allows consistent truncation where parameters don't apply).
- **Granularity trade-off is a campaign management decision, not just a naming decision:** More granular = more control (separate campaign per country, per product) but more campaigns to manage. Broader = faster management but less budget control. Budget allocation requirements (only settable at campaign level in Google Ads) should drive the decision on which parameters become campaigns vs. ad groups.
- **Always consider if there's an action to take** with the information. If a breakdown never drives a decision, don't create a campaign for it — the naming convention should reflect what you'll actually report and optimise on.
- **Three misleading data scenarios from naming failures:** (1) Mixed granularity per parameter (chairs at UK level but not USA level — makes product comparison impossible); (2) Inconsistent field values (`USA` vs `US` = two data silos); (3) Same field name for different parameters (`H` for both "high margin" and "high priority" — creates false groupings when filtering).

## Notable Quotes / Data Points

> "Naming conventions are important because they will impact how you manage your accounts and how you report on your results."

> "If you can not put your naming convention in writing, at best, you have an uncompleted naming convention."

- Cross-channel example shows 9 campaign names covering Social, Display, Search, Amazon with consistent agency + universal parameters, platform-unique parameters at the end.
- RLSA search campaigns use `RET` (retargeting) — same field meaning as Social retargeting but different technical execution. Consistent field naming across channels despite different mechanics.

## Wiki Pages Updated

- [[campaign-naming-conventions]] — parameters/fields/separators/anchors vocabulary; granularity trade-off framework; misleading data failure modes; agency structural hierarchy

## Gaps / Follow-up

- The anchor concept (disambiguating identical field values across parameters) is underexplored in all other sources — worth building into Acqura's TIP taxonomy documentation explicitly.
- The "actions you can take" principle (don't report what you can't act on) maps directly to Acqura's IABI framework — worth cross-referencing.
