---
name: Campaign Naming Conventions
type: concept
category: framework
tags: [campaign-naming, taxonomy, utm, creative-id, data-governance, tip-taxonomy]
sources: 6
last_updated: 2026-04-25
---

# Campaign Naming Conventions

## Definition

A campaign naming convention is a structured, machine-readable taxonomy that encodes marketing metadata (channel, objective, audience, creative attributes, date) into campaign, ad set, and ad names in a consistent, parseable format. It is a **data schema encoded into a string** — not a labelling system, not organisational tidiness. The purpose is retrieval, grouping, and cross-system data joining. "Final_v2_really_final.mp4" is storytelling. `cr00142|pricingproof|hook01|vid|9x16|v03` is data.

## Why It Matters for Acqura

Campaign ID governance is Acqura's **Tier 1 core deliverable** — the "T" in TIP taxonomy. It is the prerequisite data infrastructure before any GTI intelligence output can be trusted. Inconsistent naming produces fragmented, un-joinable data; GTI recommendations built on that data are asymmetrically informed at best, wrong at worst.

Beyond methodology, this cluster reveals a **commoditisation risk**: AI-powered governance tools (Improvado, Trackingplan) now auto-validate and correct campaign names across 500+ sources in real time. The manual consulting value of "Campaign ID governance setup" has a closing window. Acqura's defensible position is the intelligence layer built *on top of* the clean taxonomy — not the governance setup itself.

## How It Works

### The 4-Layer Hierarchy

Each layer answers different questions. Most clients only name at the campaign level and lose the analytical value of the ad layer.

| Layer | Answers | Example |
|---|---|---|
| **Asset file** | What is this creative? Which format variants group together? | `2026-01-13|motion|us|en|pricingproof|hook01|30s|9x16|cr00142|v03.mp4` |
| **Ad name** | What concept, hook, format, version? | `cr00142|pricingproof|hook01|vid|9x16|v03` |
| **Ad set / group** | Who are we targeting? Where? How bidding? | `pros|broad|18-55|pur|auto|lowest|us|en` |
| **Campaign** | What is the strategic goal, funnel stage, market, timeframe? | `sales|pros|evergreen|us|en|2026-01-13` |

### Two Schema Architectures

**Positional (delimiter-based):**
`US_FA_TOFU_NewBrandImage_Aug2024`
- Pro: readable, fast to scan, widely used
- Con: missing field shifts all subsequent fields; order is critical; can only add fields at the end

**Key-value pair:**
`country*US_ds*FA_funnel*TOFU_theme*NewBrandImage_start*Aug2024`
- Pro: order-independent; missing fields don't corrupt others; new fields can be inserted anywhere
- Con: longer strings; requires parsing logic; harder to scan visually

**Practitioner consensus:** positional for platform-level names (human-readable); key-value for UTM parameters (parsing correctness matters more). Either way, pick one and document it — mixing creates a new class of errors.

### Stable Creative ID — The Most Underappreciated Infrastructure Piece

A client-owned creative ID assigned *before* launch (e.g., `cr00142`) must remain stable across:
- Asset filename in DAM (Google Drive, Frame.io)
- Ad name in Meta / TikTok / Google
- `utm_content` parameter in GA4
- Backend conversion data and BI dashboard

Platform-generated IDs break when you copy or rebuild an ad. The creative ID is the **only join key** that survives across ad managers, analytics, and backend systems — enabling true cross-channel creative performance attribution.

### Structural Vocabulary (PPCHero/Brainlabs)

- **Parameter:** Label for a data type (Country, Product, Match Type) — in the convention doc, not the name itself
- **Field:** Value assigned to a parameter (USA, Chairs, Exact) — what appears in the name
- **Separator:** Single delimiter character (underscore, pipe, hyphen) — must be consistent; enables text-to-column splitting
- **Anchor:** Prefix that disambiguates identical field values across parameters (e.g., `B-Brand A` vs `_All_`) — critical for large accounts where the same value appears in multiple parameters

### Governance Layer

A convention without enforcement breaks within weeks. The three governance mechanisms:
1. **Master dictionary:** Central document of all approved parameter values. Single source of truth.
2. **URL builder:** Shared tool (Google Sheet with dropdowns + CONCATENATE) that enforces the dictionary at creation time.
3. **Automated validation:** Real-time monitoring that catches deviations (Trackingplan, Improvado) before they corrupt reporting.

### UTM Alignment

Campaign names must map to UTM parameters or analytics attribution breaks:

| UTM Parameter | Maps to | Example |
|---|---|---|
| `utm_source` | Platform | `meta`, `google`, `tiktok` |
| `utm_medium` | Channel type | `paid_social`, `cpc` |
| `utm_campaign` | Campaign name string | `sales|pros|evergreen|us|en|2026-01-13` |
| `utm_content` | Creative ID string | `cr00142|pricingproof|hook01|vid|9x16|v03` |
| `utm_id` | Stable join ID | Required for GA4 cost data import (see [[utm-tracking]]) |

## Key Practitioners / Platforms

- **Improvado** — [[improvado]] — AI-powered Marketing Data Governance; auto-validates and corrects names across 500+ sources
- **Supermetrics** — [[supermetrics]] — data connector + campaign name transformation layer for BI tools
- **Trackingplan** — UTM governance SaaS; real-time Slack alerts for UTM deviations
- **AdManage.ai** — bulk ad launch with token-based naming enforcement at creation time
- **AdAmigo.ai** — Meta AI ads tool; dynamic tokens for bulk naming; version control for creative testing

## Acqura's Angle

**TIP taxonomy = Tier 1 deliverable.** Campaign ID governance is what Acqura sets up for every Tier 1 client in weeks 1–3. It is the prerequisite for reliable GTI output. Without it, all intelligence recommendations are built on fragmented data.

**Creative ID as GTI join key.** For RTO-adjusted ROAS by campaign and creative segment (Acqura's killer Tier 1 feature for Indian D2C), the creative ID is what links ad platform spend → GA4 sessions → order management system returns. Without a stable creative ID in `utm_content`, RTO-adjusted ROAS can only be calculated at campaign level — not creative level, where the insight lives.

**Granularity principle from Brainlabs:** Only create a naming dimension you can act on. If Acqura's GTI cannot generate a different recommendation for creative A vs. creative B, encoding creative attributes in the name adds noise. Design the convention around what GTI can actually use.

**The automation threat.** Improvado's AI governance and Trackingplan's real-time validation do automatically what Acqura's Tier 1 manual governance does as a consulting service. If a client already uses either platform, Acqura's governance setup value is compressed to near-zero. Monitor pricing and capability of these tools — the defensible Tier 1 value is the intelligence interpretation above the clean data, not the clean data itself.

## Contradictions / Open Questions

- Should Acqura's TIP taxonomy use positional or key-value schema? Sources disagree on the separator character (`*` vs `:` vs `|`). Needs a decision and documented standard.
- What is the minimum viable Campaign ID governance deliverable for a Tier 1 client in a 2–3 week implementation? Which layers (4-layer hierarchy) are in-scope for Tier 1 vs. deferred to Tier 2?
- The Monetate source shows naming conventions extending to on-site personalisation experiments (A/B tests, CMS campaigns). Is Acqura's TIP taxonomy in-scope for lifecycle/CRM campaign naming (SFMC) or limited to paid media?
- At what point does Improvado or Trackingplan's automation make Acqura's manual governance service uncompetitive on price?

## Sources

- [[naming-conventions-admanage-creative-2026]] — 4-layer model; stable creative ID; decision vs. context fields; positional vs. key-value recommendation
- [[naming-conventions-trackingplan-2026]] — master dictionary; URL builder; governance automation; key-value pair architecture
- [[naming-conventions-improvado-2026]] — hierarchical three-level framework; Salesforce Campaign naming; AI governance threat; pitfall table
- [[naming-conventions-supermetrics]] — positional vs. key-value trade-off; data transformation layer (SQL, split-text, BI)
- [[naming-conventions-ppchero-brainlabs]] — parameters/fields/separators/anchors vocabulary; granularity trade-off; agency hierarchy; misleading data failure modes
- [[naming-conventions-adamigo-meta-2025]] — Meta-specific templates; version control framework; separator comparison; AI automation
