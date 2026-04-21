---
name: Cross-Cloud Identity
type: concept
category: architecture-pattern
tags: [identity, cross-cloud, experience-cloud, commerce-cloud, salesforce-identity, federation, sso]
sources: 1
last_updated: 2026-04-21
---

# Cross-Cloud Identity

## Definition
The architectural pattern for unifying customer identity across multiple Salesforce clouds (Experience Cloud, Commerce Cloud, Marketing Cloud, Service Cloud). Core principle: **Salesforce Identity as the single IdP**, with each cloud maintaining a distinct system of record for its own data domain — and federating authentication/authorization back to the central identity layer rather than synchronizing profiles.

## When to Use
- Any deployment that spans 2+ Salesforce clouds with shared customer identity (B2C scenarios with portal + commerce + service)
- When a customer must authenticate once and be recognized across storefront, self-service portal, and support channels
- When consent records and profile data need to be authoritative in one place (GDPR/CCPA compliance)

## How It Works

### Core Architecture
```
Salesforce Identity (IdP)
  ├── Experience Cloud — customer profile SoR (name, address, preferences, consent)
  ├── Commerce Cloud — shopping data SoR (orders, cart, payment, product affinity) [stub profile only]
  ├── Service Cloud — case/interaction SoR (support history, agent context)
  └── Marketing Cloud — engagement SoR (email opens, journey state, suppression)
```

### Login Flow (Experience Cloud + Commerce Cloud)
1. Customer arrives at Commerce Cloud storefront
2. Redirected to Salesforce Identity login page (hosted via Experience Cloud)
3. Customer authenticates → OAuth 2.0 token issued by Salesforce Identity
4. First login: stub profile created in Commerce Cloud, linked to Salesforce Contact ID
5. Subsequent visits: token validates identity; Commerce Cloud reads profile data from Experience Cloud via REST API on demand

### Primary Key
- **Salesforce Contact Record ID** = the universal primary key across all clouds
- Every cloud that needs to reference a customer does so by this ID
- Prevents identity divergence and enables cross-cloud reporting without data duplication

### Data Access Pattern
- **Anti-pattern**: synchronizing profile data across clouds (creates consistency conflicts, multiplies data governance burden)
- **Correct pattern**: each cloud reads from the authoritative SoR via REST API when profile data is needed
- Experience Cloud → profile attributes on demand
- Commerce Cloud → order/cart data on demand
- Service Cloud → case history on demand

## Key Constraints
- **No profile sync**: explicit architectural principle — replication leads to inconsistency; REST API reads at query time are the designed approach
- **Commerce Cloud stub profile**: Commerce Cloud creates a minimal stub on first login (linked to Salesforce Contact ID) — does not hold full profile
- **Session management**: Salesforce Identity sessions govern all connected clouds — timeout and MFA policies propagate
- **Marketing Cloud Connect**: MC does not participate in the Salesforce Identity IdP flow directly — Marketing Cloud Connect handles CRM-to-MC data replication separately

## Related Patterns / Alternatives
- **[[identity-propagation-patterns]]** (OBO/S2S/In-Task): these patterns govern agent-to-agent and service-to-service identity propagation — different scope (API call chains, not customer identity federation)
- **Data 360 identity resolution**: resolves customer identity across data sources post-ingestion for analytics/segmentation — complements cross-cloud identity but operates at the data layer, not the authentication layer
- **SAML federation**: alternative to OAuth 2.0 for enterprise SSO scenarios (employee-facing Experience Cloud sites)

## Dennis's Take
The "don't sync — federate" principle is the correct default for cross-cloud identity. The Winter '22 pattern is still architecturally sound: Salesforce Identity as IdP, Contact Record ID as primary key, REST API reads from SoR. Data 360 doesn't replace this — it adds an analytics/ML identity layer on top. For new greenfield deployments, consider whether Data 360 identity resolution should augment the federation pattern (matching known+unknown identities across channels).

## Contradictions / Open Questions
- Does the Winter '22 pattern hold for deployments with Data 360 enabled? Does Data 360's unified identity resolution change where "system of record" sits?
- How does cross-cloud identity work in headless storefront deployments (Composable Storefront / PWA Kit)?
- MFA configuration across federated clouds — is MFA enforced at Salesforce Identity level or per-cloud?

## Sources
- [[cross-cloud-identity-solution-kit]] — Full federation pattern, login flow, stub profile, REST API read anti-pattern for sync
