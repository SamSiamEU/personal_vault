---
title: Meta Content Library and API Data Dictionary
type: source
format: docs
url: raw/Meta Content Library and API Data Dictionary.md
author: Meta (official documentation)
date_published: 2025-01-01
date_ingested: 2026-04-22
tags: [meta, content-library, api, data-dictionary, facebook, instagram, research]
---

# Meta Content Library and API Data Dictionary

## Summary
Official Meta documentation describing the data fields available via the Meta Content Library web UI and Content Library API. Covers scope (which content is included), and field-by-field data dictionary for Facebook Pages, Groups, Events, Profiles, and Posts, plus equivalent Instagram objects. This is a research/academic tool — not an advertising tool. Requires specific access (researcher/institutional verification), not standard Meta Business Suite credentials.

## Key Takeaways

### Scope (What Data Is Included)
**Facebook**:
- Pages, Groups, Events; Profiles with 100+ followers or verified
- Downloadable subset: Pages with 15,000+ likes/followers; Profiles with 100+ followers or verified

**Instagram**:
- Business + creator accounts; Personal accounts with 100+ followers or verified
- Downloadable subset: Business/creator accounts with 100+ followers; Personal accounts with 100+ followers or verified

**Not included**: Private content, private groups, DMs, unverified small-follower profiles

### Key Fields Available
**Facebook Page**: name, username, about, description, page_categories, follower_count, like_count, verification_status, page_manager countries (predicted admin locations), has_active_ads, has_run_political_ads, creation_date, page name change history, page merge history

**Facebook Post**: text, creation_time, modified_time, language (ISO 639-1), like_count, love/wow/haha/sad/angry reaction counts, match_type (post_text/image_text/multimedia_text for search results), is_verified

**Facebook Group**: name, description, member_count, creation_date, name change history, admin/moderator page IDs

**Facebook Event**: name, description, going_count, interested_count, event_start/end_time, place location fields

## Wiki Pages Updated
- [[meta-platform]] — Content Library as research access path (distinct from advertising tools)

## Gaps / Follow-up
- Low direct relevance to Acqura's paid media focus — this is a transparency/research tool
- Could be useful if Acqura wants to analyze competitor brand content performance at scale (organic post engagement) — but requires researcher-level access
- Threads content mentioned as "in development, data quality may have significant variation"
