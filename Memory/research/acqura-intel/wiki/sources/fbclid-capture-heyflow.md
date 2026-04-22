---
title: How to Capture the Meta Click ID (fbclid) With Your Funnel (Heyflow)
type: source
format: article
url: raw/How to Capture the Meta Click ID (fbclid) With Your Funnel.md
author: Heyflow
date_published: 2025-01-01
date_ingested: 2026-04-22
tags: [fbclid, meta, click-id, attribution, capi, hidden-fields, crm, offline-conversions]
---

# How to Capture the Meta Click ID (fbclid) With Your Funnel (Heyflow)

## Summary
Explains the fbclid (Facebook Click Identifier) mechanism — how Meta auto-appends it to destination URLs, how to capture it via hidden form fields, and why it's essential for closing the attribution loop between Meta ad clicks and downstream CRM conversions. Written by Heyflow (no-code funnel builder) but covers universal principles applicable to any funnel tool.

## Key Takeaways
- **fbclid** = unique Meta identifier appended to destination URL when user clicks a Facebook/Instagram ad; format: `yourwebsite.com/?fbclid=IwAR2xK9...`
- Captures encoded information about which campaign, ad set, and creative generated the click
- **Capture flow**: User clicks ad → fbclid in URL → hidden form field extracts fbclid via JavaScript → form submission passes fbclid to CRM → offline conversion upload to Meta with fbclid as match key
- **fbclid vs UTMs**: complementary, not competing — fbclid = deep Meta ad-level attribution; UTMs = cross-channel context in GA4/other analytics; use both together
- Without fbclid: Meta-driven traffic appears as "direct" in Google Analytics (fbclid gets stripped during redirects) → inflated direct traffic, undervalued Meta campaigns
- **Offline conversion tracking**: captured fbclid can be sent back to Meta via CAPI as the match key for lead-to-sale attribution (qualified leads, closed deals)
- **Stronger lookalike audiences**: fbclid tied to post-click behavior gives Meta visibility into users who completed meaningful actions, not just clicked — improves retargeting precision

### Manual Implementation (Any Funnel)
1. Add hidden input field with name `fbclid` or `fb_click_id` to form
2. JavaScript reads URL query params on page load, finds fbclid value
3. JavaScript populates hidden field automatically
4. Form submission passes fbclid to CRM/analytics alongside lead data
5. Test: click through own Meta ad, verify fbclid appears in CRM records

### Common Mistakes
- **Losing fbclid during redirects**: HTTP→HTTPS redirect or tracking domain redirect strips the parameter — handle explicitly
- **Not persisting across funnel steps**: multi-step funnels must pass fbclid through each step — parameters get lost between pages
- **CRM field not mapped**: capturing fbclid in form but not mapping to CRM property = data collected, never stored
- **Overwriting on resubmissions**: some systems overwrite fbclid with empty value on second submission — prevent with conditional logic

### Best Practices
- Always store fbclid as a permanent CRM field (not session-only)
- Combine with UTM parameters: one hidden field for fbclid, one each for utm_source/medium/campaign/content/term/id
- Upload offline conversions to Meta using captured fbclid: qualified lead → demo → closed deal (with CAPI `event_id` for deduplication)
- Audit CRM records periodically for fbclid capture rate — drops indicate tracking breakage

## Notable Quotes / Data Points
> "Without fbclid tracking, your Meta advertising operates in a fog. You know leads are coming in, but you can't definitively connect them to specific campaigns, audiences, or creatives."

## Wiki Pages Updated
- [[meta-conversions-api]] — fbclid mechanism and role in CAPI deduplication
- [[meta-platform]] — fbclid capture as part of tracking architecture
- [[utm-tracking]] — fbclid and UTMs as complementary, not competing

## Gaps / Follow-up
- Heyflow's own CAPI native integration (mentioned at end) — sends conversion events to Meta in real-time including fbclid matching; worth checking if Heyflow is in any Acqura client's stack
- The `gclid` (Google Click ID) follows the same pattern — parallel implementation for Google Ads
