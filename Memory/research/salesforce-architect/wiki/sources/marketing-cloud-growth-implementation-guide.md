---
title: Marketing Cloud Growth/Advanced Edition Implementation Guide (Summer '25)
type: source
format: docs
url: raw/mktg_implementation_guide.pdf
author: Salesforce
date_published: 2025-05-12
date_ingested: 2026-04-21
tags: [marketing-cloud, marketing-cloud-growth, marketing-cloud-advanced, data-cloud, email, sms, whatsapp, consent, agentforce, einstein]
---

# Marketing Cloud Growth/Advanced Edition Implementation Guide (Summer '25)

## Summary
Salesforce's official admin and implementation guide for **Marketing Cloud Growth and Advanced Edition** — the new native-platform Marketing Cloud product (distinct from legacy Marketing Cloud / Email Studio / Journey Builder). This product requires Data Cloud as a prerequisite and runs entirely on the Salesforce Platform. Campaigns are Flow-based, channels use Unified Messaging, and content lives in Salesforce CMS. Covers full setup lifecycle from Data Kits through consent, channels, reporting, AI features, and scoring.

## Key Takeaways

### Architecture — What Makes This Different from Legacy MC
- **Requires Data Cloud**: identity resolution, segmentation, and behavioral tracking all run through Data Cloud — not optional
- **Native Salesforce Platform**: no separate MC infrastructure; shares Salesforce CRM org; permission sets on Salesforce users
- **Campaigns = Flows**: campaign orchestration built entirely on Flow Builder (not Journey Builder); marketers build "Campaign Flows"
- **Channels = Unified Messaging**: email, SMS, WhatsApp via Unified Messaging framework (not Email Studio / Mobile Studio)
- **Content in Salesforce CMS**: email content in CMS workspaces (not Content Builder); landing pages via Digital Experiences Sites framework
- **Consent in Data Cloud DMOs**: consent data stored in `ConsentAuditTrail` and `MessagingConsent` DMOs; consent checks enforced before sends
- **Scoring in Data Cloud**: engagement + fit scoring runs on Unified Individual DMOs; results surface as Calculated Insights on lead/contact pages

### Setup Architecture (Key Dependencies)
1. Enable Data Cloud (prerequisite — cannot skip)
2. Create Salesforce CRM Connector in Data Cloud
3. Install Data Kits (MarketingSetup_General, ConsentObjects, Flows Integration, Email/SMS/WhatsApp Channel Data Kits)
4. Deploy Data Streams (some auto-deploy; others require manual deployment by Data Cloud admin)
5. Configure Identity Resolution Rulesets (Individual → Normalized Email match rule; add lead-to-contact and device-to-known custom rules)
6. Configure channels (DKIM for email, code registration for SMS, WhatsApp Business Account)
7. Set up web tracking (Salesforce Interactions SDK or consent banner snippet)
8. Configure scoring rules (engagement + fit; up to 30 rules each)
9. Activate AI features (Einstein STO, Engagement Scoring, Metrics Guard, Agentforce)

### Data Kits and Data Streams
| Data Kit | Package Name | Purpose |
|----------|-------------|---------|
| Marketing Setup Objects | MarketingSetup_General (+ SMSAddOn_General) | Core DMOs for marketing assets and consent |
| Consent Objects | UnifiedMessagingConsent | ConsentAuditTrail + MessagingConsent data streams |
| Flows Integration | Salesforce Data Cloud - Flow Integration | Flow Run data streams for campaign tracking |
| Email Channel | MessagingEventsEmailEngagement | Email engagement events |
| SMS Channel | MessagingEventsSms | SMS engagement events (add-on only) |
| WhatsApp Channel | UnifiedWhatsAppPackage | WhatsApp engagement events (add-on only) |

### Consent Architecture
- Default: consent stored in Data Cloud DMOs via `UnifiedMessagingConsent` data kit
- Communication Subscriptions: create one per marketing category (e.g., Product Updates); subscriber must opt-in per channel type
- Consent import: CSV per channel + subscription + status; contact point must already exist (can't create new contacts via import)
- Consent validation: enforced on each send; can be disabled (marketer assumes compliance responsibility)
- Preference pages: default pages for email/SMS/WhatsApp; customizable; immediately published when saved

### Identity Resolution for Marketing
- Recommended: one active ruleset for Individual, one for Account
- Add two custom rules to Individual ruleset: `lead-to-contact` (handles lead conversion) and `device-to-known` (web tracking attribution)
- Normalized Email is the default match rule for Individual
- Identity resolution consumes Data Cloud credits — keep to minimum active rulesets

### Web Tracking Architecture
- Landing pages: Sites framework (`Marketing Landing Pages` site runs behind the scenes — never add content to it)
- Consent banner: `sfmc_consent` cookie (365 days); `_sfid_${domainHash}` cookie (730 days) for visitor ID
- External sites: Install External Tracking Data Kit → create Website Connector → deploy Behavioral Events + Identity data streams → add script to website `<head>`; map UTM parameters to Data Cloud fields
- Tracked data: page views, form submissions, link clicks, button clicks

### Scoring Architecture
- Two components: Engagement score (behavioral signals) + Fit score (demographic match) → combined into Overall Marketing Score (normalized 0–100)
- Default engagement rules: form-submit (+10), anchor-click (+3), button-click (+3), email CLICK (+3), SUBSCRIBE (+5), UNSUBSCRIBE (-5), bot/error events (-5)
- Up to 30 engagement + 30 fit rules; max 10 conditions per rule; can use condition groups
- Scores stored as Calculated Insights → `People_Score__c`, `Engagement__Score__c`, `Fit_Score__c`; surfaced via Data Cloud Profile Insights component on lead/contact pages
- Account scoring: includes intent-to-buy toggle; account-level scores can't be added to Account page layouts

### AI Features
| Feature | Edition | Type | Notes |
|---------|---------|------|-------|
| Agentforce (Campaign Briefs, Campaign Designer) | Growth + Advanced | Generative AI | Draft briefs, campaigns, subject lines from prompts |
| Einstein Segment Creation | Growth + Advanced | Generative AI | AI-assisted segment building |
| Einstein Send Time Optimization (STO) | Growth + Advanced | Predictive | Optimal send time per individual; global model (opt-in for Growth, opt-in/out for Advanced); trains on 90 days of email history |
| Einstein Metrics Guard | Growth + Advanced | Predictive | Bot click/open filtering; global model; time-series analysis |
| Einstein Engagement Scoring | Advanced only | Predictive | Contact-level engagement prediction; requires Data Graph for Flow integration |
| Einstein Engagement Frequency | Advanced only | Predictive | Optimal contact frequency prediction; requires Data Graph for Flow integration |

### Limits
| Resource | Growth Edition | Advanced Edition |
|---------|--------------|----------------|
| Active Flows | 500 | 750 |
| Saved Flows | 50,000 | 50,000 |
| Email Credits/Year | 180,000 | 360,000 |
| Engagement Scoring Rules | 30 | 30 |
| Fit Scoring Rules | 30 | 30 |

### Permission Sets
- **Marketing Cloud Admin**: access to Salesforce Setup, Agentforce Admin, Prompt Template Manager, full campaign/segment/flow control
- **Marketing Cloud Manager**: non-admin full campaign/segment/flow control + Agentforce/Prompt Template use
- **Identity-Licensed Users**: can access MC via Salesforce SSO; assign Marketing Cloud Manager + Tableau Next Included App Business User permission sets; cannot access Setup

### Key Differences from Legacy Marketing Cloud
| Aspect | Legacy MC (Email Studio / Journey Builder) | New MC Growth/Advanced |
|--------|------------------------------------------|-----------------------|
| Infrastructure | Separate Salesforce platform | Native Salesforce Platform |
| Data Cloud | Optional / integration layer | Required prerequisite |
| Journey orchestration | Journey Builder | Campaign Flows (Flow Builder) |
| Email authoring | Content Builder | Salesforce CMS |
| Scripting | AMPScript / SSJS | Not applicable (Flow + merge fields) |
| Data model | Data Extensions, Subscriber Key | Salesforce Objects + Data Cloud DMOs |
| Consent | MC-native suppression lists | Data Cloud DMOs (ConsentAuditTrail) |
| Channel setup | Studio-specific configuration | Unified Messaging framework |

## Notable Quotes / Data Points
- "Before you can access all the required and additional settings, you must first go to Basic Settings and enable Marketing Cloud." — Data Cloud is gated prerequisite
- "To succesfully complete all of the prerequisites, you must first enable Data Cloud."
- Einstein Metrics Guard: "reduces the risk of false positive and false negative results" for bot-click filtering
- "Customers that have Data Cloud One enabled and use Marketing Cloud Growth or Advanced edition operate from, store, and process customer data in the same location as the customer's Data Cloud home organization"

## Wiki Pages Updated
- [[marketing-cloud]] — Added section on Marketing Cloud Growth/Advanced vs Legacy MC
- [[data-360]] — MC Growth/Advanced uses Data Cloud natively; consent stored in DMOs; scoring via Calculated Insights

## Gaps / Follow-up
- Marketing Cloud Advanced Edition only features (Engagement Scoring, Engagement Frequency) need deeper coverage
- Multi-org scenario: how Marketing Cloud Growth/Advanced integrates with Data Cloud One companion org setup
- Pricing/credit model for Growth vs Advanced vs Legacy MC not documented
- Campaign Flows architecture (how they differ from standard Flows, available Flow elements) not covered in depth
