---
title: How to Use the Meta Ad Library API to Scrape Ad Data (Swipekit)
type: source
format: article
url: raw/How to use the Meta ad library API to scrape ad data?.md
author: Swipekit
date_published: 2025-01-01
date_ingested: 2026-04-22
tags: [meta, ad-library, api, competitor-research, graph-api, swipekit]
---

# How to Use the Meta Ad Library API to Scrape Ad Data (Swipekit)

## Summary
Practical guide to accessing the Meta Ad Library via the Graph API for competitive research. Written by Swipekit (an ad-saving Chrome extension). Covers access requirements, two key identifiers (adId vs pageId), and search capabilities. Includes critical limitation: API only works for EU-targeted ads, Brazil (limited), and political/social cause ads.

## Key Takeaways

### Critical Limitation
> "The API only works for the ads running in the European Union, Brazil (limited scope) or if they are tagged as political/social issue ads."

This means the official API is **not useful** for competitive research on US advertisers running standard product/service ads. For US market competitor research, web scraping tools (Swipekit, AdLibraryHelper) are the practical path.

### Two Key IDs
- **adId**: unique identifier for a specific ad in the Ad Library
- **pageId**: pagination cursor; also used to retrieve all ads from a specific Facebook Page; NOT directly exposed in the Ad Library UI

### How to Get pageId
1. Navigate to the ad's individual URL in the Ad Library
2. Copy the URL parameter `view_all_page_id` — that's the pageId
3. Or: use Swipekit Chrome extension → hold Ctrl/Cmd + click Save button → pageId shown above button

### API Endpoints (Graph API)
- Base: `ads_archive?ad_reached_countries=EU&search_terms=<term>`
- Filter params: `ad_active_status` (ACTIVE/INACTIVE/ALL), `ad_delivery_date_min/max`, `media_type` (ALL/IMAGE/VIDEO/MEME/NONE), `languages` (array of language codes)
- Can't search by adId directly — must paginate from pageId

### Access Requirements
1. Create app in Meta Developer Console (consumer type)
2. Verify identity via Meta's verification page (ID document upload — took hours for author)
3. Verification is account-level, not app-level — all your apps get access once verified
4. Access tokens expire; extend to 3 months via Graph API Explorer; automate rotation for production

### npm Wrapper (Node.js)
`npm install facebookadlibrary` — wrapper around the Ad Library API; simplifies pagination and search:
- `findByPageId(pageId)` — all ads from a page
- `findByAdId(adId, pageId)` — find specific ad (requires both IDs)
- `findBySearchTerm('skincare')` — broad search; accepts filter params

## Notable Quotes / Data Points
- Swipekit has worked with the ad library for 3+ years
- Token default expiry is short; Graph API Explorer extends to 3 months

## Wiki Pages Updated
- [[meta-ad-library]] — concept page created, API limitations documented
- [[meta-platform]] — Ad Library API limitations noted in entity page

## Gaps / Follow-up
- Branded content / influencer post discovery (collab posts) mentioned as a separate topic deserving its own article
- The API's EU limitation is a significant gap — if Acqura wants competitive intelligence for US clients, scraping is the only viable path (and comes with ToS risk)
