---
name: Marketing Cloud (Salesforce Marketing Cloud)
type: entity
category: salesforce-cloud
tags: [marketing-cloud, email, sms, whatsapp, journey-builder, ampscript, ssjs, cdp-adjacent]
sources: 3
last_updated: 2026-04-21
---

# Marketing Cloud (Salesforce Marketing Cloud)

## What It Is
Salesforce's B2C marketing automation platform. Handles outbound multi-channel communications (email, SMS, WhatsApp, push), journey orchestration, behavioral segmentation, and campaign analytics. Positioned as the engagement execution layer — where Data 360 segments are activated and where journeys are run. Distinct from Data 360: Marketing Cloud runs campaigns; Data 360 builds audiences and resolves identity.

## Relevance to Architecture Work
- Integration hub for cross-cloud customer engagement — connects to Sales Cloud, Service Cloud, Commerce Cloud, and Data 360
- Email Studio is the standard choice for high-volume transactional and marketing email (replaces Commerce Cloud native email)
- Journey Builder is the orchestration tool for multi-step engagement workflows
- Scripting environment (AMPScript + SSJS) enables dynamic personalization and CRM data access at send time

## Key Capabilities
- **Journey Builder**: multi-step journey orchestration with entry/exit conditions, wait steps, decision splits, goal tracking
- **Email Studio**: email authoring, deliverability management (IP warming, reputation monitoring), A/B testing, triggered sends
- **Mobile Studio**: SMS, push notifications, WhatsApp messaging
- **Data Extensions**: tabular data storage for subscribers, products, orders — the MC equivalent of Salesforce objects for campaign data
- **AMPScript**: proprietary scripting language for dynamic email/landing page personalization; CRM data access via `RetrieveSalesforceObjects`
- **SSJS (Server-Side JavaScript)**: more capable scripting language (arrays, objects, try/catch) that can interoperate with AMPScript via `Platform.Function.TreatAsContent()`
- **Marketing Cloud Connect**: bi-directional integration with Salesforce CRM — replicates Contacts/Leads/Campaigns to MC, exposes email engagement back to CRM Activity Timeline, enables journey triggers from CRM events
- **Automation Studio**: scheduled batch automation for data feeds, imports, and sends
- **Analytics Builder**: email and journey performance reporting

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
- How does Data 360 activation (Real-Time Data Actions) interact with Marketing Cloud Journey Builder triggers? Does Data 360 replace Automation Studio for journey entry?
- With Agentforce Conversational Agents now available, does Einstein Bots in WhatsApp flows get replaced? What's the migration path?
- Marketing Cloud "on Salesforce Platform" (MCOPS) — is this a real product direction that unifies MC data model with Salesforce objects?

## Sources
- [[conversational-campaigns-whatsapp-solution-kit]] — WhatsApp flow, Digital Engagement SKU, 24-hour session window, Channel-Object Linking
- [[cross-cloud-data-models-solution-kit]] — MC as system of record for engagement history; Marketing Cloud Connect; SFTP connector pattern with Commerce Cloud
- [[transactional-email-solution-kit]] — Email Studio as replacement for SFCC native email; SFTP data feed pattern; triggered send performance considerations
- [[marketing-cloud-engage-tips]] — AMPScript/SSJS scripting patterns, TreatAsContent bridge, error handling template
