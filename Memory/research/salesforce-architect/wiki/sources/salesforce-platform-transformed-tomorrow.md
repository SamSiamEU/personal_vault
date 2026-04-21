---
title: The Salesforce Platform — Transformed for Tomorrow
type: source
format: article
url: raw/The Salesforce Platform - Transformed for Tomorrow  Get Started with Fundamentals.md
author: Salesforce (Chief Architect office)
date_published: 2024-01-01
date_ingested: 2026-04-21
tags: [salesforce-platform, hyperforce, architecture, agentforce, evolution, metadata]
---

# The Salesforce Platform — Transformed for Tomorrow

## Summary
Strategic architectural white paper co-authored with Salesforce's top engineers describing the platform's transformation from the original Force.com (2008) through Hyperforce to the current AI/agentic platform. Covers 6 architectural principles, 10 platform layers, Hyperforce infrastructure deep-dive (Instances/Cells/Supercells, security, FinOps, availability), and how the platform has evolved to support Agentforce at scale. Read first 150 of ~1,000 lines.

## Key Takeaways
- **6 architectural principles**: Enterprise-Grade Trust, Multitenant, Metadata-Driven, API First, Open and Interoperable, Agentic
- **4 key transformations**: Hyperforce adoption, monolithic → microservices, Data 360 + Lakehouse alongside relational DB, AI/ML/agentic integration
- 95%+ of customers migrated to Hyperforce as of Dreamforce 2024
- **10 platform layers**: Hyperforce, Metadata Framework, Data, AI, App Platform Services, Business Capabilities, APIs + API Management, User/Dev Experience, Integration, Apps and Industries
- **Hyperforce Instances**: mapped to AWS Availability Regions; operate independently; 3+ AZ replication; Cells = scale units (≈ traditional Salesforce instances); Supercells = larger blast radius groupings
- **Operating Zones**: Grouped Hyperforce Instances for data residency (EU Operating Zone for GDPR)
- **Zero-Trust**: mTLS between services, just-in-time access, short-lived private keys, PKI with certificate revocation, phishing-resistant MFA for production access
- **FinOps**: COIN score tracks optimization; Unit Cost Explorer; Compute Savings Plans + Spot + ODCR; blue/green = ~1 min/year maintenance

## Notable Quotes / Data Points
- "Currently, more than 95% of our customers have transitioned to this new platform"
- "Hyperforce's modern CI/CD pipelines and blue/green application releases minimize application maintenance periods to just one minute a year"
- Chief Architect quote: platform evolution "without significant disruptions, thanks to robust abstractions"

## Wiki Pages Updated
- [[salesforce-platform]] — 6 principles, 10 layers, Hyperforce fundamentals
- [[hyperforce]] — Instances/Cells/Supercells, Operating Zones, zero-trust security, FinOps

## Gaps / Follow-up
- Only read first 150 lines (~34K token file); Metadata Framework deep-dive, AI layer specifics, App Platform Services, and Integration layer details not yet read
- Agentforce platform integration (how Agentforce sits within the 10 layers) needs further reading
