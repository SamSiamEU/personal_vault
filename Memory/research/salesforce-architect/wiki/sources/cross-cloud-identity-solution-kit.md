---
title: Seamless Cross-Cloud Identity Solution Kit
type: source
format: pdf
url: raw/seamless_cross_cloud_identity_solution_kit.pdf
author: Salesforce
date_published: 2021-01-01
date_ingested: 2026-04-21
tags: [cross-cloud, identity, experience-cloud, commerce-cloud, salesforce-identity, solution-kit, winter-22]
---

# Seamless Cross-Cloud Identity Solution Kit

## Summary
Winter '22 solution kit describing how to federate customer identity across Experience Cloud and Salesforce B2B/B2C Commerce Cloud using Salesforce Identity as the central IdP. Core architectural principle: each cloud owns a distinct system of record (SoR) — Experience Cloud for profile, Commerce Cloud for shopping data — and identity federation ties them together without profile synchronization.

## Key Takeaways

### Core Architecture
- **Salesforce Identity as IdP**: single source of truth for authentication across all clouds
- **Experience Cloud** = system of record for customer profile data (name, address, preferences, consent)
- **Commerce Cloud** = system of record for shopping data (orders, payment methods, wishlists, product affinity)
- No profile sync between clouds — use REST APIs to read from each system's own SoR at query time

### Login Flow
1. Customer authenticates via Salesforce Identity (Experience Cloud login page)
2. OAuth token issued; stub profile created in B2B Commerce Cloud on first login
3. Commerce Cloud stub profile linked to Salesforce Contact via shared identity token
4. Subsequent visits: Salesforce Identity token used to retrieve Commerce Cloud session

### Design Principles
- **Don't sync — federate**: duplicating profile data across clouds creates consistency problems; read from SoR instead
- **Salesforce Contact Record ID** as primary key — single identifier that all clouds reference
- Experience Cloud handles profile enrichment (preference center, consent management)
- Commerce Cloud handles transactional enrichment (purchase history, saved payment, cart state)

### Integration Points
- Salesforce Identity OAuth 2.0 flows connecting Experience Cloud ↔ Commerce Cloud
- REST API calls from Commerce Cloud storefront to Experience Cloud for profile data
- Commerce Cloud hooks for login/registration events to trigger Salesforce Identity flows

## Notable Quotes / Data Points
- "Do not synchronize profiles across clouds" — explicit anti-pattern called out
- Winter '22 (2021) — pre-Data 360; identity federation predates Data Cloud identity resolution
- B2B Commerce focus but principles apply to B2C Commerce with adaptations

## Wiki Pages Updated
- [[cross-cloud-identity]] (new concept — to be created)
- [[experience-cloud]] (new entity — to be created)

## Gaps / Follow-up
- Read first 200 lines (pdftotext); full technical implementation details may be in remainder
- B2C Commerce variant likely similar but session/cart handling differs
- How does this pattern evolve with Data 360 identity resolution now available? (open question)
