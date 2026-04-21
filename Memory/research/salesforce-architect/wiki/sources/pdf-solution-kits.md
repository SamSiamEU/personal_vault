---
title: Salesforce Solution Kits (PDF Collection)
type: source
format: report
url: raw/[multiple PDFs]
author: Salesforce
date_published: 2024-2025
date_ingested: 2026-04-21
tags: [solution-kits, agentforce, cross-cloud, identity, commerce, whatsapp]
---

# Salesforce Solution Kits (PDF Collection)

## Summary
Collection of Salesforce Solution Kit PDFs that were found in raw/ but could not be read due to missing poppler-utils PDF rendering library. These are Salesforce reference implementation guides for specific cross-cloud use cases. Based on filenames, they cover: Agentforce customer implementation, SFCC roadmap, Digital Wallet in SDO, cross-cloud data models, cross-cloud identity, conversational campaigns (WhatsApp), and transactional email.

## Files in this batch
- `agentforce_implementation_customer.pdf` — Agentforce implementation guide for customers
- `SFCC Roadmap items.pdf` — Salesforce Commerce Cloud roadmap
- `Solution Kit - Digital Wallet in SDO.pdf` — Digital wallet reference implementation in Salesforce Demo Org
- `cross_cloud_data_models_solution_kit.pdf` — Cross-cloud data model patterns
- `seamless_cross_cloud_identity_solution_kit.pdf` — Cross-cloud identity architecture
- `conversational_campaigns_whatsapp_solution_kit.pdf` — WhatsApp conversational campaigns
- `transactional_email_solution_kit.pdf` — Transactional email architecture
- `Marketing Cloud Engage tips.docx` — Marketing Cloud Engage practical tips

## Key Takeaways
- Content not yet ingested due to PDF rendering limitation
- Based on titles: cross-cloud identity and data models would be highest architectural value
- Digital Wallet in SDO appears to be a demo/reference implementation (possible own IP classification once reviewed)
- WhatsApp conversational campaigns aligns with Conversational Agent patterns already documented

## Wiki Pages Updated
- None yet — pending PDF ingestion capability

## Gaps / Follow-up
- **ACTION**: Install poppler-utils (`brew install poppler`) to enable PDF reading, then re-ingest all PDFs
- Cross-cloud identity solution kit likely has deep dive on identity propagation patterns — high priority to read
- Agentforce implementation customer guide may contain production patterns not in other sources
