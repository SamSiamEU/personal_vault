---
name: Commerce Cloud (Salesforce B2C/B2B Commerce)
type: entity
category: salesforce-cloud
tags: [commerce-cloud, sfcc, sfra, b2c-commerce, b2b-commerce, ecommerce, storefront]
sources: 3
last_updated: 2026-04-21
---

# Commerce Cloud (Salesforce B2C/B2B Commerce)

## What It Is
Salesforce's ecommerce platform in two variants: **B2C Commerce** (formerly Demandware/SFCC — high-traffic consumer storefronts, SFRA cartridge-based) and **B2B Commerce** (native Salesforce object-based, account-level buying). In cross-cloud architectures, Commerce Cloud is the system of record for shopping data: orders, cart state, payment methods, product affinity, and transaction history. Profile data lives in Experience Cloud/CRM — Commerce Cloud holds the transactional layer.

## Relevance to Architecture Work
- **Shopping data SoR**: Commerce Cloud owns order history, payment profiles, cart/wishlist state, and product affinity. Do not replicate this to CRM — surface via REST API where needed.
- **Integration topology**: B2C Commerce integrates with Salesforce ecosystem via connectors (B2C → Service Cloud Connector, B2C → MC Connector), SFTP data feeds, and REST APIs. Not natively on Salesforce platform — separate infrastructure.
- **Transactional email**: Commerce Cloud's native email is limited — replace with Marketing Cloud Email Studio for deliverability, personalization, and suppression management.
- **Identity dependency**: Commerce Cloud federates identity to Salesforce Identity (via Experience Cloud as IdP) — stub profile created on first login, not a full profile sync.

## Key Capabilities
- **SFRA (Storefront Reference Architecture)**: B2C Commerce cartridge-based storefront framework; customized via cartridges (controllers, templates, models)
- **Order Management**: full OMS capability including order lifecycle, fulfillment, returns, exchanges
- **Product Catalog**: multi-locale, multi-currency product catalog with categories, attributes, pricing
- **Promotions & Campaigns**: promotion engine, discount codes, tiered pricing
- **B2C → Service Cloud Connector**: syncs Commerce orders to Service Cloud for agent context; orders appear on Contact/Account record
- **B2C → Marketing Cloud Connector**: syncs catalog/order/customer data to MC data extensions; hooks for post-purchase journey triggers
- **Salesforce Identity Integration**: OAuth 2.0 federation to Salesforce Identity for SSO; stub profile creation on first login
- **Einstein Recommendations**: ML-based product recommendation engine embedded in storefronts
- **B2B Commerce (native)**: built on Salesforce platform (Account/Contract/Order objects); account-level buying, negotiated pricing, approval workflows

## Licensing / Pricing
- B2C Commerce: GMV-based pricing (% of gross merchandise value); platform fee scales with revenue
- B2B Commerce: user-license based; can be included in certain Sales Cloud configurations
- Connector accelerators: typically included; SFTP/API connector may require additional setup
- [detailed rates unknown]

## Strengths
- B2C Commerce: proven high-traffic consumer storefront platform (handles major retailers at holiday peak)
- SFRA cartridge architecture: modular, supports rapid customization without core modification
- Order management embedded — not a bolt-on
- Connector accelerators reduce custom integration build for common cross-cloud data flows
- Einstein Recommendations integrated natively

## Weaknesses / Gaps
- **B2C Commerce is NOT on Salesforce platform**: different infrastructure, different data model, different security model — cross-cloud integration always involves API/connector boundary
- SFTP data feeds (for Marketing Cloud) are batch — not real-time; delays in transactional email triggers
- Native email capabilities are limited — Marketing Cloud replacement is a standard implementation pattern
- SFRA customization can become complex at scale — cartridge conflicts, override chains, version management
- B2B Commerce (native) lacks some capabilities that B2C Commerce has at scale (product catalog depth, high-volume catalog performance)

## Known Gotchas
- **Don't sync profiles to Commerce Cloud**: Experience Cloud is the profile SoR; Commerce Cloud stub profile should link to Salesforce Contact ID, not duplicate profile data
- **SFTP volume at peak**: design MC data feed exports to handle holiday/flash-sale peak order volumes; triggered send queues can back up at volume
- **GMV-based licensing**: pricing model means Commerce Cloud cost scales directly with revenue — forecast carefully for high-growth clients
- **B2C Commerce ≠ Salesforce platform**: governor limits, sharing model, and Apex don't apply — different runtime constraints
- **Winter '22 solution kits**: cross-cloud connector patterns documented in Winter '22 kits are foundational but predate Data 360 — some Heroku aggregation patterns are now replaceable with Data Cloud DMOs

## Contradictions / Open Questions
- How does Data 360 activation (Real-Time Data Actions) replace or complement the SFTP → Marketing Cloud pattern for order-triggered emails?
- SFCC Roadmap PDF is unreadable (image-based) — product direction for Commerce Cloud is not covered in current sources
- B2B Commerce vs. CPQ for complex configure-price-quote scenarios in B2B context — architectural boundary not documented

## Sources
- [[cross-cloud-identity-solution-kit]] — Commerce Cloud as shopping data SoR, stub profile pattern, Salesforce Identity federation
- [[cross-cloud-data-models-solution-kit]] — SoR ownership model, B2C connectors (Service Cloud, Marketing Cloud), Contact Record ID as primary key
- [[transactional-email-solution-kit]] — SFTP data feed pattern, B2C → MC Connector hooks, triggered send design for transactional email
