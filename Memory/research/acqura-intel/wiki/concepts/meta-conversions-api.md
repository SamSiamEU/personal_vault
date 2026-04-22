---
name: Meta Conversions API (CAPI) & Server-Side Tracking
type: concept
category: tactic
tags: [capi, server-side-tracking, meta, facebook, pixel, emq, deduplication, fbclid, first-party-data]
sources: 6
last_updated: 2026-04-22
---

# Meta Conversions API (CAPI) & Server-Side Tracking

## Definition
Meta Conversions API (CAPI) is a server-to-server tracking method that sends conversion events directly from a business's server to Meta's servers, bypassing the user's browser entirely. Unlike the Meta Pixel (which runs JavaScript in the browser), CAPI is immune to ad blockers, iOS privacy restrictions, and third-party cookie deprecation. It is now the baseline requirement for any serious Meta advertiser — not an optional enhancement.

**2026 state**: Third-party cookies fully deprecated in Chrome (2025). Pixel-only tracking captures 50–65% of actual conversions. CAPI brings total capture to 95%+. The legacy Offline Conversions API was discontinued May 2025; CAPI handles all conversion signals (web, offline, app) through a unified endpoint.

## Why It Matters for Acqura
- **This is the data layer Acqura sits above.** If a client's CAPI is broken or missing, their conversion data is incomplete — any intelligence Acqura builds on top is unreliable. Tracking health audit is a necessary prerequisite for GTI work.
- **EMQ score is the data quality proxy.** Before Acqura can make attribution or budget recommendations, the client needs EMQ 6+ (ideally 8+) across their key conversion events. Low EMQ = the algorithm is flying blind = Acqura's insights are noise.
- **CAPI reveals the first-party data gap.** The parameters needed for high EMQ (hashed email, phone, customer ID) require first-party data collection at checkout/lead form. Clients who don't capture email at conversion have a structural data problem — a GTI entry point.
- **The CAPI remediation opportunity**: Many clients are on pixel-only or have broken CAPI. Fixing this before selling intelligence is a billable setup phase. "Fix your data, then get intelligence from it" is a natural Acqura positioning.

## How It Works

### Core Architecture (Dual Tracking)
```
User clicks Meta ad
    ↓ (Pixel fires in browser — can be blocked)
User completes purchase / lead / event
    ↓
Server confirms transaction
    ↓ (CAPI fires: server → Meta API endpoint)
Meta receives both events
    ↓ (Deduplication via event_id — 48-hour window)
Single conversion counted from 2 sources
    ↓
Algorithm optimization (Advantage+, lookalike, retargeting)
```

### Key Components

**Meta Pixel (client-side)**
- JavaScript fires in browser on page events (PageView, AddToCart, InitiateCheckout, Purchase)
- Real-time; blocked by ~40% of browsers via ad blockers or iOS ATT
- Still required — provides real-time browser context CAPI can't capture

**CAPI (server-side)**
- HTTP request from your server to `graph.facebook.com` after server-confirmed conversion
- Not blockable — no browser dependency
- Handles web, offline/POS, app events via same endpoint
- `action_source` parameter tells Meta where event happened (`website`, `physical_store`, `app`)

**Deduplication**
- Send same `event_id` on both Pixel and CAPI for the same event
- Meta discards duplicates received within 48 hours
- Pattern: `event_id = "Purchase:{order_id}"` — must be a string, not a number
- Events Manager shows "1 event from 2 sources" when working correctly

**fbclid (Facebook Click ID)**
- Unique identifier Meta appends to destination URLs when a user clicks a Meta ad
- Appears as `?fbclid=IwAR2xK9...` in the landing page URL
- Capture in hidden form field → pass to CRM → upload offline conversions with fbclid as match key
- Together with UTM parameters: fbclid = deep Meta attribution, UTMs = cross-channel context in GA4
- Lost during redirects if not handled explicitly

### Event Match Quality (EMQ)
Scored 0–10 in Meta Events Manager. Measures how well your server events match to Meta user accounts.

| Score | Quality | Impact |
|-------|---------|--------|
| 0–4 | Poor | Meta struggles to match; limited optimization |
| 4–6 | Fair | Basic matching; below standard |
| 6–8 | Good | Solid matching; effective optimization |
| 8–10 | Excellent | Maximum matching; optimal ad delivery |

**How to improve EMQ:**
- Add hashed email (`em`, SHA256) → typically +4 points — biggest single impact
- Add hashed phone (`ph`, E.164 format, SHA256) → +3 points
- Include `fbp` (Facebook browser cookie) and `fbc` (fbclid value)
- Add address components (city, state, zip, country) → +1.5 points
- Include `external_id` (your CRM customer ID)

**Hashing rules**: SHA256, lowercase, trim whitespace before hashing. Never send raw PII — hash first.

### Setup Methods Comparison

| Method | Setup Time | Cost | Technical Skill | Best For |
|--------|-----------|------|-----------------|----------|
| Partner Integration (Shopify, WooCommerce) | 1–2 hours | Free | None | Single-channel e-commerce |
| GTM Server-Side | 4–8 hours | $10–50/mo hosting | Intermediate | Multi-platform marketers |
| Direct API (custom code) | 20–40 hours | Dev time | Advanced | Enterprises, custom stacks |
| Gateway Service (managed) | 2–4 hours | $20–400+/mo | Basic | Agencies, multi-client |

### Required CAPI Parameters
- `event_name` — the conversion event (Purchase, Lead, AddToCart)
- `event_time` — UNIX timestamp (UTC)
- `action_source` — where event happened

### Recommended Parameters (for high EMQ)
- `em` — hashed email (SHA256) — biggest EMQ impact
- `ph` — hashed phone (E.164, SHA256)
- `fn`, `ln` — hashed first/last name
- `client_ip_address` — do NOT hash
- `client_user_agent` — do NOT hash
- `fbc` — fbclid cookie value — do NOT hash
- `fbp` — Facebook browser ID cookie — do NOT hash
- `external_id` — your internal customer ID (hash recommended)
- `event_id` — for deduplication with Pixel

### Key Performance Benchmarks
- Pixel-only → 50–65% conversion capture
- Pixel + CAPI → 95%+ conversion capture
- After CAPI implementation: +20–40% increase in reported conversions (Meta Ads Manager)
- High EMQ setup: 13% lower cost per result + 19% more attributed purchase events (Meta data)
- Typical ROAS improvement over 30–60 days: 10–25% as algorithm absorbs better signals

## Key Practitioners / Platforms
- **Weld** — Reverse-ETL platform with native CAPI integration; SQL-model → CAPI sync; best for omni-channel brands with data in warehouse
- **AdAmigo** — AI-powered Meta optimization tool that layers on CAPI data to make autonomous budget recommendations
- **Heyflow** — Funnel builder with automatic fbclid + UTM parameter capture; no-code CAPI native integration
- **Shopify** — Native CAPI integration via Meta official app (no code required for single-channel Shopify stores)

## Acqura's Angle
CAPI is infrastructure Acqura's clients must have working before GTI adds value. Three-phase framing:

1. **Diagnose**: Check EMQ scores across key events. If below 6, broken tracking is costing them money right now — this is a quick win to demonstrate.
2. **Fix**: CAPI implementation or improvement. Not Acqura's core product, but a billable setup phase or partner referral.
3. **Optimize**: Once data is clean (EMQ 8+, 95%+ capture), Acqura's GTI can produce reliable cross-channel recommendations.

This mirrors the existing triangulation framework (MTA + MMM + incrementality) — CAPI is what makes first-party MTA reliable. Acqura should assume broken tracking is the default state for SMB clients, not an edge case.

## Contradictions / Open Questions
- If Meta's Advantage+ consumes CAPI data directly and optimizes automatically, what incremental value does an external intelligence layer (Acqura's GTI) add for pure Meta campaigns? Acqura needs a clear answer: GTI adds value across channels (Meta + Google + programmatic), not just within Meta.
- At what EMQ threshold does Advantage+ perform well enough that human optimization (or GTI) is unnecessary? Is there a ceiling?

## Sources
- [[server-side-tracking-meta-capi-intro]] — conceptual intro, Pixel vs CAPI comparison table
- [[meta-capi-setup-guide-adamigo]] — setup walk-through, key stats (20% purchase boost, Diptyque 67% increase)
- [[meta-capi-implementation-guide-2026-weld]] — 2026 definitive guide: cookie deprecation context, 95%+ capture stat, use cases, parameter reference, deduplication
- [[meta-capi-complete-guide-adsuploader]] — 4 setup methods, EMQ scoring table, 15 troubleshooting issues
- [[fbclid-capture-heyflow]] — fbclid mechanism and capture implementation
- [[utm-tracking]] — UTM + fbclid used together for complete attribution
