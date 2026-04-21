---
title: Data 360 Security Architecture
type: source
format: article
url: raw/Data 360 Security Architecture  Data 360 and Integration.md
author: Salesforce Architect
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [data-360, security, abac, cedar, encryption, hyperforce, compliance]
---

# Data 360 Security Architecture

## Summary
Technical reference for Data 360's security model. Covers the shared responsibility framework, Hyperforce zero-trust infrastructure, ABAC/CEDAR for runtime authorization (PIP/PDP/PEP triad), OLS/FLS/RLS/DDM for data access controls, data spaces for logical isolation, named and external credentials for API access, CMK/BYOK for encryption key management, AWS PrivateLink for private connectivity, and compliance certifications (ISO 27001, SOC 1/2/3, FedRAMP, HIPAA).

## Key Takeaways
- **Shared responsibility**: Salesforce owns infrastructure security; customers own data governance, access control, and configuration
- **Hyperforce zero-trust**: All services behind mTLS; least privilege; no data leaves boundary without explicit policy
- **ABAC/CEDAR**: Policy-based access control at runtime — PIP (Policy Information Point), PDP (Policy Decision Point), PEP (Policy Enforcement Point); more granular than RBAC
- **OLS/FLS/RLS**: Object-level, field-level, row-level security — layered access restriction within Data 360
- **DDM (Dynamic Data Masking)**: Masks sensitive fields (PII, financial) at query time based on user context
- **Data spaces**: Logical tenant isolation within an org; scope clean rooms, AI workloads, regional data sets
- **CMK/BYOK**: Customer controls encryption keys; key rotation without data loss; hardware security module backing
- **AWS PrivateLink**: Private connectivity from customer VPC to Data 360 — eliminates public internet exposure
- Compliance certifications: ISO 27001, SOC 1/2/3, FedRAMP High, HIPAA, PCI DSS, GDPR

## Notable Quotes / Data Points
- ABAC/CEDAR allows attribute-based policies — claims from OBO tokens can drive authorization decisions at Data 360 query layer
- Data spaces also serve as clean room isolation boundaries — design data spaces aligned with partnership and regulatory domains

## Wiki Pages Updated
- [[data-360]] — ABAC/CEDAR, OLS/FLS/RLS, CMK/BYOK, compliance certifications
- [[data-clean-rooms]] — Data spaces as clean room isolation

## Gaps / Follow-up
- CEDAR policy language details not covered — needs separate research for implementing complex ABAC policies
- Interaction between ABAC/CEDAR policies and Agentforce agent identity claims not fully specified
