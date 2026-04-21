---
title: Platform Sharing Architecture
type: source
format: article
url: raw/Platform Sharing Architecture  Get Started with Fundamentals.md
author: Salesforce Architect
date_published: 2024-01-01
date_ingested: 2026-04-21
tags: [sharing, security, owd, role-hierarchy, apex-sharing, territory]
---

# Platform Sharing Architecture

## Summary
Advanced reference guide for Salesforce's sharing model covering all data access components: OWD, Role Hierarchy, Public Groups, Owner-Based Sharing Rules, Criteria-Based Sharing Rules, Guest User Rules, Manual Sharing, Teams, Territory Management, Apex Managed Sharing, Restriction Rules, and Implicit Sharing. Includes real-world use cases mapped to solutions and a troubleshooting flow.

## Key Takeaways
- 9-layer access model from most restrictive (OWD) to programmatic (Apex Managed Sharing) + Restriction Rules (opposite direction)
- High-volume users (Customer Community, HVCP) bypass standard sharing model — use sharing sets or share groups instead
- Role hierarchy: max 10 branch levels, max 5,000 roles (Spring '21+), max 25,000 internal roles best practice; peers in same role do NOT share access
- Owner-based sharing rules: 300/object; criteria-based: 50/object; guest user rules: 50/object (combined with criteria-based)
- Territory management: separate from role hierarchy; use for matrix sales models; don't duplicate role hierarchy in territories
- Apex Managed Sharing: use when no declarative option works; custom sharing reasons on custom objects; performance concern at large volumes
- Restriction rules: narrow access further; max 2 active/object (Enterprise) or 5 (Performance/Unlimited); apply to list views, reports, SOQL, SOSL
- Implicit sharing: automatic, non-configurable; account access from contact/opp/case; does NOT apply to custom objects
- Performance: data skew (>10K children per parent), ownership skew (>10K records per owner), OWD recalculation — all require careful architecture planning

## Notable Quotes / Data Points
- Account hierarchy does NOT provide data access — common architect mistake
- Defer sharing calculations feature (support-enabled) critical for bulk changes on large orgs
- Best practice: keep public groups to ≤100,000 org-wide; ≤5 nesting levels

## Wiki Pages Updated
- [[sharing-model]] — Complete sharing model reference
- [[salesforce-platform]] — Sharing model as platform access control layer

## Gaps / Follow-up
- Interaction between Data 360 ABAC/CEDAR and Salesforce CRM sharing model for hybrid queries not documented
