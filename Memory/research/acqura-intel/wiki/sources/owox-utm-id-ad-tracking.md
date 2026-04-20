---
title: "UTM ID: Why You Must Include It in Your Ad Tracking"
type: source
format: article
url: https://www.owox.com/blog/articles/utm-id/
author: OWOX
date_published: 2023-04-01
date_ingested: 2026-04-20
tags: [utm, ga4, tracking, cost-import, attribution]
---

# UTM ID: Why You Must Include It in Your Ad Tracking

## Summary

A technical how-to from OWOX explaining that `utm_id` — long an optional UTM parameter — became a required field in Google Analytics 4 for importing non-Google ad cost data. Without it, cost imports succeed but produce a 0% match rate, meaning clicks, impressions, and ROAS remain blank for non-Google campaigns. The article walks through the four required UTM tags, how to populate `utm_id`, and how to verify it's working. Source has a vendor angle (OWOX sells automated cost import).

## Key Takeaways

- `utm_id` is mandatory in GA4 for non-Google cost data import — not optional as it was in Universal Analytics
- The four required tags for GA4 cost import: `utm_campaign`, `utm_source`, `utm_medium`, `utm_id`
- Missing `utm_id` produces a silent failure: import succeeds with 0% match rate, no error unless `campaign_id` is literally empty
- Workaround when ad platforms don't expose Campaign ID via API: duplicate the Campaign Name value into Campaign ID
- Verification: build a custom GA4 Exploration report using the "Session campaign ID" dimension
- OWOX positions itself as the tool to automate this import process across ad platforms

## Notable Quotes / Data Points

> "All traffic that was not tagged with utm_id will not be matched with what we uploaded in the file."

- GA4 error on empty campaign_id: *"Invalid empty value detected on row campaign_id. A non-empty value must be set."*
- Google's Campaign URL Builder supports `utm_id` field

## Wiki Pages Updated

- [[owox]] — entity page created
- [[utm-tracking]] — concept page created
- [[ga4-cost-data-import]] — concept page created

## Gaps / Follow-up

- Which ad platforms expose Campaign ID via API vs. which require manual/name-based workaround?
- How do GA4 cost imports compare to server-side attribution solutions (e.g. Northbeam, Triple Whale)?
- OWOX pricing and positioning — is this a point solution or a broader analytics platform?
