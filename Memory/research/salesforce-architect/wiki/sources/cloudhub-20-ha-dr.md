---
title: CloudHub 2.0 High Availability and Disaster Recovery
type: source
format: article
url: raw/CloudHub 2.0 High Availability and Disaster Recovery  Data 360 and Integration.md
author: Gulal Kumar, Ajay Nagaraju (Salesforce)
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [mulesoft, cloudhub, ha, dr, aws, availability, disaster-recovery]
---

# CloudHub 2.0 High Availability and Disaster Recovery

## Summary
Technical guide for designing HA and DR architectures for MuleSoft CloudHub 2.0 workloads. Covers the outage scenario matrix (replica down, AZ down, region down), Object Store V2 regional constraints, ingress controller behavior, three DR configuration options (Active-Active, Warm Standby, Cold Standby), networking architecture (vanity domains, Route 53), and stateless integration design principles.

## Key Takeaways
- CloudHub 2.0 runs on AWS; tied to AWS regional availability; no native multi-region HA
- Single replica: restarts in another AZ automatically (~2-15 min); multi-replica: spread across AZs by default
- **Region down**: No automatic recovery — requires pre-configured failover design
- **US East is the control plane**: US East outage = Runtime Manager unavailable globally; apps in other regions keep running but can't be managed or redeployed
- **Object Store V2 is region-bound**: Stays in original deployment region even if app moves; not available in cross-region DR scenarios — externalize state for DR
- **Private space = regional**: Must be pre-provisioned in DR region before disaster; cannot be created during outage
- **Three DR options**: Active-Active (concurrent multi-region with Route 53 latency/failover routing), Warm Standby (passive region pre-warmed, ready to start), Cold Standby (passive region provisioned on-demand via CI/CD)
- Vanity domains + Route 53 (or equivalent CDN) required for cross-region traffic routing
- Stateless integration design principle: no transactional state in MuleSoft infrastructure; externalize to DB/queue

## Notable Quotes / Data Points
- "CloudHub 2.0 does not support multi-region HA or DR out of the box"
- Active-Active: Route 53 latency routing detects unhealthy primary and routes to DR; fast failover
- Warm Standby: lower cost than Active-Active; some startup time required for passive region

## Wiki Pages Updated
- [[mulesoft]] — CloudHub 2.0 HA/DR constraints, Object Store V2 regional limitations
- [[hyperforce]] — Cross-reference for US East control plane dependency

## Gaps / Follow-up
- Exact RTO/RPO numbers for each DR option not provided — need to validate with MuleSoft Support
- Anypoint MQ cross-region failover not covered in this guide (noted as out of scope; link to separate Anypoint MQ failover docs)
