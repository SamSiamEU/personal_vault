---
name: Marketing Cloud (Salesforce Marketing Cloud)
type: entity
category: salesforce-cloud
tags: [marketing-cloud, email, sms, whatsapp, journey-builder, ampscript, ssjs, cdp-adjacent, marketing-cloud-growth]
sources: 4
last_updated: 2026-04-21
---

# Marketing Cloud (Salesforce Marketing Cloud)

> **Important architectural distinction**: There are two very different products called "Marketing Cloud":
> - **Legacy Marketing Cloud** (Email Studio / Journey Builder / AMPScript / SSJS) — separate Salesforce infrastructure, Data Cloud optional
> - **Marketing Cloud Growth / Advanced Edition** — native Salesforce Platform, Data Cloud **required**, campaigns via Flow Builder
> Both are covered below. When an architect says "Marketing Cloud," clarify which variant.

## What It Is
Salesforce's B2C marketing automation platform family. The legacy platform (Email Studio, Journey Builder) handles outbound multi-channel communications, journey orchestration, and campaign analytics on separate Salesforce infrastructure. The new platform (Growth/Advanced Edition) runs natively on the Salesforce Platform with Data Cloud as a required component — campaigns are Flow-based and channels use the Unified Messaging framework.

## Relevance to Architecture Work
- Integration hub for cross-cloud customer engagement — connects to Sales Cloud, Service Cloud, Commerce Cloud, and Data 360
- Email Studio is the standard choice for high-volume transactional and marketing email (replaces Commerce Cloud native email)
- Journey Builder is the orchestration tool for multi-step engagement workflows
- Scripting environment (AMPScript + SSJS) enables dynamic personalization and CRM data access at send time

## Key Capabilities — Legacy Marketing Cloud (Email Studio / Journey Builder)
- **Journey Builder**: multi-step journey orchestration with entry/exit conditions, wait steps, decision splits, goal tracking
- **Email Studio**: email authoring, deliverability management (IP warming, reputation monitoring), A/B testing, triggered sends
- **Mobile Studio**: SMS, push notifications, WhatsApp messaging
- **Data Extensions**: tabular data storage for subscribers, products, orders — the MC equivalent of Salesforce objects for campaign data
- **AMPScript**: proprietary scripting language for dynamic email/landing page personalization; CRM data access via `RetrieveSalesforceObjects`
- **SSJS (Server-Side JavaScript)**: more capable scripting language (arrays, objects, try/catch) that can interoperate with AMPScript via `Platform.Function.TreatAsContent()`
- **Marketing Cloud Connect**: bi-directional integration with Salesforce CRM — replicates Contacts/Leads/Campaigns to MC, exposes email engagement back to CRM Activity Timeline, enables journey triggers from CRM events
- **Automation Studio**: scheduled batch automation for data feeds, imports, and sends
- **Analytics Builder**: email and journey performance reporting

## Key Capabilities — Marketing Cloud Growth / Advanced Edition (New)
Requires Salesforce Enterprise/Unlimited + Data Cloud. Runs natively on Salesforce Platform.

- **Campaign Flows**: Flow Builder-based campaign orchestration (replaces Journey Builder); segment-triggered, form-triggered, automation event-triggered, data graph change-triggered flows
- **Unified Messaging**: single framework for email, SMS, WhatsApp sends; DKIM-authenticated email domains; no Email Studio
- **Salesforce CMS**: email and landing page content in CMS workspaces; landing pages via Digital Experiences Sites framework
- **Data Kits**: packaged Data Cloud objects/streams for marketing — install once, reuse across campaigns (Email/SMS/WhatsApp/Consent/Flows Integration kits)
- **Consent in Data Cloud**: `ConsentAuditTrail` + `MessagingConsent` DMOs; communication subscriptions per channel type; consent import via CSV; preference pages per channel
- **Scoring**: engagement + fit scoring on Unified Individual DMOs; Calculated Insights exposed as `People_Score__c`/`Engagement__Score__c`/`Fit_Score__c` on lead/contact pages; up to 30 rules each type
- **Web Tracking**: Salesforce Interactions SDK + consent banner; `_sfid_${domainHash}` cookie for visitor ID; behavioral events in Data Cloud; UTM parameter mapping
- **AI — Einstein Send Time Optimization (STO)**: optimal send time per individual; global model (opt-in for Growth); analyzes 90 days of email history
- **AI — Einstein Metrics Guard**: bot click/open filtering; time-series analysis; global model
- **AI — Einstein Engagement Scoring** (Advanced only): contact-level engagement prediction; requires Data Graph for Flow integration
- **AI — Einstein Engagement Frequency** (Advanced only): optimal contact frequency prediction
- **Agentforce**: Campaign Briefs, Campaign Designer, Einstein Segment Creation — generative AI tools for marketers
- **Limits**: Growth = 500 active Flows / 180K email credits/yr; Advanced = 750 active Flows / 360K email credits/yr

## Licensing / Pricing
- Editions: Basic, Pro, Corporate, Enterprise — functionality and sending volume tiers
- Corporate/Enterprise required for full Journey Builder and Mobile Activation
- Digital Engagement SKU: required for WhatsApp, in-app messaging, and real-time messaging channels
- Mobile Activation SKU: required for SMS sending
- Marketing Cloud Connect: requires Salesforce CRM license on the connected org

## Strengths
- Industry-leading email deliverability tooling (IP warming, reputation management, bounce handling)
- Global suppression list management across all programs — strong compliance posture
- Unified view of email engagement (opens, clicks, unsubscribes) surfaced back to Salesforce CRM
- AMPScript + SSJS scripting enables sophisticated dynamic content and CRM-integrated personalization at send time
- Journey Builder handles complex multi-step B2C engagement workflows

## Weaknesses / Gaps
- Data model is MC-specific (Data Extensions, subscriber keys) — requires learning curve and different paradigm from Salesforce objects
- AMPScript is proprietary — not transferable outside MC
- SFTP-based data feed pattern (for Commerce Cloud integration) is batch, not real-time
- MC is separate from the Salesforce core platform — different infrastructure, different data residency controls, separate compliance certifications
- Pre-Data 360 segmentation tools (Contact Builder, Audience Builder) are limited compared to Data 360 segmentation engine

## Known Gotchas
- **RetrieveSalesforceObjects in SSJS**: requires Marketing Cloud Connect — can't call CRM data from scripting without it
- **Triggered send queue**: high-volume events (flash sales, mass order confirmations) can overwhelm triggered send queue — design with send classification and priority queuing
- **24-hour WhatsApp session window**: after expiry, outbound messages must use pre-approved WhatsApp Message Templates — can't send freeform; approval process through Meta Business Manager
- **Data Extension shared folder prefix**: when accessing shared folder DEs via SSJS/AMPScript, must prefix name with `ENT.`
- **TreatAsContent performance**: embedding AMPScript inside SSJS has a performance cost — only use where no SSJS equivalent exists; avoid in high-volume send-time scripts

## Contradictions / Open Questions
- How does Data 360 activation (Real-Time Data Actions) interact with legacy MC Journey Builder triggers? Does Data 360 replace Automation Studio for journey entry?
- With Agentforce Conversational Agents now available, does Einstein Bots in WhatsApp flows get replaced? What's the migration path?
- What is the migration path from legacy Marketing Cloud (Email Studio / Journey Builder) to Marketing Cloud Growth/Advanced Edition? Are they parallel products for different segments, or is Growth/Advanced the planned replacement?
- MC Growth/Advanced Edition targets Enterprise/Unlimited Salesforce orgs — what's the equivalent for customers on Core or Pro who need email marketing?
- How does Marketing Cloud Connect (legacy) interact with MC Growth/Advanced in a mixed-install scenario?

## Sources
- [[conversational-campaigns-whatsapp-solution-kit]] — WhatsApp flow, Digital Engagement SKU, 24-hour session window, Channel-Object Linking
- [[cross-cloud-data-models-solution-kit]] — MC as system of record for engagement history; Marketing Cloud Connect; SFTP connector pattern with Commerce Cloud
- [[transactional-email-solution-kit]] — Email Studio as replacement for SFCC native email; SFTP data feed pattern; triggered send performance considerations
- [[marketing-cloud-engage-tips]] — AMPScript/SSJS scripting patterns, TreatAsContent bridge, error handling template
- [[marketing-cloud-growth-implementation-guide]] — Full setup guide for MC Growth/Advanced Edition: Data Kits, consent architecture, channels, scoring, AI features, limits
