---
title: Conversational Campaigns (WhatsApp) Solution Kit
type: source
format: pdf
url: raw/conversational_campaigns_whatsapp_solution_kit.pdf
author: Salesforce
date_published: 2021-01-01
date_ingested: 2026-04-21
tags: [marketing-cloud, service-cloud, whatsapp, einstein-bots, messaging, solution-kit, winter-22]
---

# Conversational Campaigns (WhatsApp) Solution Kit

## Summary
Winter '22 solution kit for SMS-to-WhatsApp promotional campaign workflow. Marketing Cloud sends promotional SMS with a WhatsApp link → customer clicks → WhatsApp session opens → Einstein Bots handle initial interaction → Service Cloud agent takes over in Messaging Console if needed → case closed. Covers the WhatsApp 24-hour session window constraint and required product SKUs.

## Key Takeaways

### End-to-End Flow
1. **Marketing Cloud**: sends promotional SMS containing a WhatsApp deep link (via Journey Builder or Automation Studio)
2. **Customer action**: clicks link → WhatsApp opens → session initiated with Salesforce WhatsApp Business Account
3. **Einstein Bots**: handles initial interaction — collects intent, gathers qualifying information, attempts self-service resolution
4. **Escalation**: if bot cannot resolve → routes to live agent via Omni-Channel
5. **Service Cloud Messaging Console**: agent handles conversation in Omni-Channel inbox
6. **Case management**: Messaging User record created in Service Cloud; Channel-Object Linking connects Messaging User to Contact; case closed when resolved

### WhatsApp 24-Hour Session Window Constraint
- WhatsApp Business API: once a customer initiates a conversation, a 24-hour session window opens
- Within the window: free-form messages allowed in both directions
- **After 24 hours**: outbound messages must use pre-approved WhatsApp Message Templates
- Approved templates sent via Flow or Process Builder — not freeform
- Architectural implication: re-engagement campaigns after session expiry require template approval process (WhatsApp Business Manager)

### Service Cloud Integration
- **Messaging User record**: created automatically when customer starts WhatsApp conversation
- **Channel-Object Linking (COL)**: links Messaging User → Contact (or Lead) for identity resolution
- Agent sees full conversation history + linked Contact record in Messaging Console
- Case created manually or automatically via Flow on first message

### Required Products / SKUs
- Marketing Cloud (Corporate or Enterprise tier)
- Mobile Activation SKU (for SMS sending)
- Service Cloud (any edition)
- Digital Engagement SKU (for WhatsApp/Messaging channels)
- WhatsApp Business Account (via Meta Business Manager)

## Notable Quotes / Data Points
- Winter '22 (2021) — Einstein Bots predates Agentforce; with Agentforce now available, Einstein Bots role in this flow can be replaced by Agentforce Conversational Agent
- 24-hour window constraint is a WhatsApp platform constraint, not a Salesforce constraint — applies to all WhatsApp Business integrations
- Channel-Object Linking is the mechanism for tying messaging identities to CRM records across all digital channels (not just WhatsApp)

## Wiki Pages Updated
- [[marketing-cloud]] (new entity — to be created)
- [[async-processing-patterns]] — Channel-Object Linking as identity resolution mechanism for messaging channels

## Gaps / Follow-up
- Read first 150 lines (pdftotext); detailed Flow/Process Builder configuration for template sending in remainder
- Agentforce Conversational Agent as modern replacement for Einstein Bots in this flow — architecture would be cleaner
- How does Data 360 segmentation feed into Marketing Cloud journey triggers for this use case?
