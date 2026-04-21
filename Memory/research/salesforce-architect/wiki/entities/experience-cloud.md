---
name: Experience Cloud (Salesforce Experience Cloud)
type: entity
category: salesforce-cloud
tags: [experience-cloud, communities, digital-experience, portal, identity, b2c]
sources: 1
last_updated: 2026-04-21
---

# Experience Cloud (Salesforce Experience Cloud)

## What It Is
Salesforce's platform for building digital experiences — customer portals, partner communities, self-service sites, and branded web storefronts. Built on top of the core Salesforce platform (shares the same org, objects, and sharing model). In cross-cloud B2C architectures, Experience Cloud serves as the customer-facing web layer and is typically the system of record for customer profile data (name, address, preferences, consent).

## Relevance to Architecture Work
- **Identity hub in cross-cloud architectures**: When using Salesforce Identity as IdP, Experience Cloud hosts the login/registration UX and holds the authoritative customer profile. Commerce Cloud and other clouds federate identity back to it.
- **Customer profile SoR**: In multi-cloud deployments, Experience Cloud (via Salesforce Contact/Person Account) is the canonical source for profile attributes. Do not replicate profile data to other clouds — read via API from Experience Cloud.
- **Consent management**: Experience Cloud (backed by Salesforce CRM) is the appropriate home for consent records — important for GDPR/CCPA compliance architecture.

## Key Capabilities
- **LWR (Lightning Web Runtime) and Aura sites**: two site frameworks; LWR is newer, preferred for new builds
- **Self-Service Portal**: case deflection via Knowledge Articles, community Q&A, case submission
- **Partner Community**: deal registration, MDF, partner portal with role-based data access
- **Commerce Portal**: storefront layer for B2B Commerce (Account-based buying)
- **Salesforce Identity integration**: acts as IdP or SP; hosts OAuth 2.0 flows; handles customer login/registration/SSO
- **CMS Content**: native content management for portal pages, articles, media
- **Sharing model**: Experience Cloud extends Salesforce sharing model — guest user, authenticated user, portal user visibility controlled via sharing rules and profiles

## Licensing / Pricing
- Pricing by site type and login method (member-based licensing vs. login-based)
- Customer Community: basic self-service portal
- Customer Community Plus: + reporting, advanced sharing
- Partner Community: partner portal with Salesforce object access
- Digital Experiences add-on: enhanced LWR, headless capabilities
- [pricing details unknown beyond tier names]

## Strengths
- Tight integration with Salesforce CRM data — no ETL needed for portal data
- Salesforce Identity natively integrated — federated SSO with external systems out of the box
- Sharing model extends naturally to portal users — complex B2B partner data access scenarios manageable
- LWR sites support headless/headless-hybrid deployments for frontend flexibility

## Weaknesses / Gaps
- Not a full-featured CMS — content management capabilities are limited compared to standalone CMS platforms
- Performance can lag for high-traffic, anonymous public sites — not designed for high-volume B2C traffic (Commerce Cloud SFRA is better suited)
- LWR vs Aura migration: older Aura sites require rebuild to move to LWR — architectural commitment at build time

## Known Gotchas
- **Guest user sharing**: by default, guest users have very restricted data access — requires explicit sharing rule configuration; easy to accidentally over-expose data if misconfigured
- **Profile sync anti-pattern**: in cross-cloud identity architectures, do NOT sync profile data from Experience Cloud to Commerce Cloud — use REST API reads from Experience Cloud as SoR instead
- **Session management**: Experience Cloud sessions are Salesforce sessions — timeout and security policies apply; important for federated identity flows with Commerce Cloud
- **Digital Experiences licensing**: headless Experience Cloud (API-only, custom frontend) requires careful licensing review — not all capabilities included in base Community licenses

## Contradictions / Open Questions
- How does Experience Cloud identity federation evolve with Data 360 identity resolution? Does the Salesforce Identity IdP pattern remain the right approach, or does Data 360 unify identity at the data layer instead?
- Experience Cloud as headless CMS vs. Commerce Cloud storefront: where is the boundary in a B2C deployment?

## Sources
- [[cross-cloud-identity-solution-kit]] — Identity federation: Experience Cloud as customer profile SoR, login flow via Salesforce Identity, REST API read pattern (don't sync), stub profile creation in Commerce Cloud
