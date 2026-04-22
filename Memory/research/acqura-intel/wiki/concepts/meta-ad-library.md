---
name: Meta Ad Library & Competitor Research
type: concept
category: tactic
tags: [meta, ad-library, competitor-research, ad-intelligence, api]
sources: 1
last_updated: 2026-04-22
---

# Meta Ad Library & Competitor Research

## Definition
The Meta Ad Library is a public database of all active and recently inactive ads running across Facebook, Instagram, and Meta's other platforms. It provides basic ad creative and targeting metadata for transparency purposes. The Ad Library API provides programmatic access but with significant geographic restrictions.

## Why It Matters for Acqura
Understanding what competitor ads are running is a key input for growth strategy recommendations. However, the Meta Ad Library's API limitations mean that direct API-based competitive intelligence is severely restricted — knowing this prevents overselling automated competitor research as a GTI feature.

## How It Works

### Web UI (Ad Library)
- Search by advertiser name, keyword, or category
- View active ads with basic metrics: platforms, start date, impressions range, estimated spend range
- Available globally; no account required for basic access

### Ad Library API (Programmatic)
Access via Graph API after identity verification. Key capabilities:
- `ads_archive` endpoint: search ads by keyword, advertiser page, date range, media type, language
- Filter by: `ad_active_status`, `ad_delivery_date_min/max`, `media_type` (ALL/IMAGE/VIDEO/MEME/NONE)
- Two IDs: `adId` (unique ad identifier) and `pageId` (pagination cursor — also used to find page's ads)

**Critical caveat — geographic restriction**:
> The API only returns ads targeted to the European Union, Brazil (limited scope), or ads categorized as political/social cause ads.

US-only advertisers' ads are **not accessible via the API** — only via the web UI or scraping tools.

### For Non-EU Competitors: Scraping Tools
Commercial tools fill the API gap:
- **Swipekit** — Chrome extension + platform for saving and organizing ads from the Ad Library; exposes `pageId` from the UI for programmatic use
- **AdLibraryHelper** — Chrome extension for filtering and saving Meta Ad Library ads
- These tools scrape the web UI rather than using the API, so they work globally

### Implementation Notes (API)
- Requires Meta Developer app + identity verification (identity document upload)
- Access tokens expire; extend to 3 months via Graph API Explorer; automate rotation via cron for production use
- Can't search by `adId` directly — must get `pageId` from URL, then paginate
- npm wrapper `facebookadlibrary` (Node.js) simplifies pagination and search

## Key Constraints
- API data limited to EU + Brazil (limited) + political/social cause ads
- No ad asset (creative, image, video) access via API — assets require scraping
- No advertiser-level performance data (spend, ROAS, CTR) — only estimated impression ranges
- `pageId` not exposed in Ad Library UI — must infer from URL parameter `view_all_page_id`

## Acqura's Angle
The API restriction means automated competitive intelligence on US advertisers via the official API is not viable. For competitive research, point clients toward web UI + Swipekit/AdLibraryHelper. Don't build GTI features that assume API-based ad intelligence unless targeting EU clients specifically.

The bigger opportunity: Meta Ad Library shows *what* competitors are running but not *what's performing*. Acqura's GTI layer adds the performance intelligence that Ad Library can't provide.

## Contradictions / Open Questions
- Will Meta expand Ad Library API access beyond EU/political ads? EU's Digital Services Act transparency requirements drove the current scope — other markets may follow.

## Sources
- [[meta-ad-library-api-swipekit]] — API access guide, pageId/adId mechanics, geographic restrictions, npm wrapper
