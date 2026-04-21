---
title: Data 360 Clean Rooms
type: source
format: article
url: raw/Data 360 Clean Rooms  Data 360 and Integration.md
author: Yugandhar Bora, Birendra Kumar Singh, Priyanka Kshirsagar (Salesforce)
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [data-360, clean-rooms, privacy, zero-copy, pets, collaboration]
---

# Data 360 Clean Rooms

## Summary
Comprehensive guide to Data 360's clean room capabilities covering the architectural evolution from "bunker" to federated models, Privacy-Enhancing Technologies (PETs), use cases across AdTech/retail/financial/healthcare, Salesforce-specific implementation architecture, deployment workflow, and operational governance. Positions clean rooms as core enterprise infrastructure for AI-driven, privacy-compliant multi-party collaboration.

## Key Takeaways
- Traditional "bunker" clean rooms: data copied to third party; modern Salesforce model: federated, zero-copy, computation at source
- **Three personas**: Privacy/compliance officers (governance focus), data scientists (utility/ML focus), business users/marketers (TTV focus)
- **PETs are mandatory system-level controls**: Differential Privacy (mathematical noise + budget tracking), Secure Identifier Alignment (deterministic hashing), Aggregation Thresholds (minimum record count, non-overridable), Result Suppression
- **Use cases**: AdTech measurement (66% of orgs use clean rooms — 2025 State of Retail Media), CPG-Retailer POC collaboration, cross-bank fraud detection, clinical trial patient recruitment
- **Data 360 pipeline**: Connect → Persist → Harmonize → Unify → Derive Insights → Act (activation closed loop)
- **Activation Gap closed**: Insights flow directly to Marketing Cloud, ad platforms without raw data ever leaving governed boundary
- **Audit DMO**: Immutable audit trail; captures query, timestamp, requester, policy applied
- **Digital Wallet**: Real-time consumption tracking; configure alerts at 50%/75%/90% thresholds
- **Einstein Trust Layer as airlock**: Zero-data-retention for LLM calls on clean room data; PII masking

## Notable Quotes / Data Points
- "66% of organizations now use clean rooms in some capacity" (2025 State of Retail Media)
- WPP acquisition of InfoSum reflects clean rooms becoming mainstream infrastructure
- "Zero-copy doesn't eliminate compute costs. While physical duplication is removed, execution occurs at the source system"
- Cross-cloud: native AWS Clean Rooms interoperability for multi-cloud enterprises

## Wiki Pages Updated
- [[data-clean-rooms]] — Full clean room architecture, PETs, use cases, deployment workflow
- [[data-360]] — Clean room as native Data 360 capability

## Gaps / Follow-up
- Privacy budget management in practice (how to track and reset differential privacy budget) not fully specified
- Clean room pricing/credit consumption vs. standard Data 360 not detailed
