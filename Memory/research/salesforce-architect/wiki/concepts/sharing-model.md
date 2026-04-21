---
name: Salesforce Sharing Model
type: concept
category: governance
tags: [sharing, security, owd, role-hierarchy, apex-sharing, territory]
sources: 1
last_updated: 2026-04-21
---

# Salesforce Sharing Model

## Definition
Salesforce's layered record-level access control framework. Controls which users can see and edit which records through a hierarchy of declarative and programmatic mechanisms, from organization-wide defaults (most restrictive) through roles, sharing rules, teams, and programmatic overrides.

## When to Use
Apply sharing model design in every Salesforce implementation. It's the first architectural decision after defining the data model — getting it wrong causes expensive rework. Critical for:
- Multi-geography or multi-BU implementations
- Regulated industries (financial services, healthcare) where data segregation is mandatory
- Large data volume orgs (2M+ accounts) where recalculation performance matters

## How It Works

### Layered Architecture (most restrictive → most permissive)
```
1. Profile/Permission Set (object-level access)
2. OWD — Organization-Wide Defaults (baseline record access)
3. Role Hierarchy (manager inherits subordinate access)
4. Sharing Rules (owner-based or criteria-based exceptions)
5. Teams (account/opportunity/case team membership)
6. Territory Management (matrix sales hierarchies)
7. Manual Sharing (ad-hoc record-by-record)
8. Apex Managed Sharing (programmatic for complex scenarios)
9. Restriction Rules (narrow access further — opposite direction)
```

### Core Mechanisms

**OWD (Organization-Wide Defaults)**
- Set baseline: Public Read/Write, Public Read Only, Private, Controlled by Parent
- Use most restrictive setting — sharing opens up from here
- OWD changes trigger sharing recalculation — can be very slow for large orgs
- `Grant Access Using Hierarchies` setting on custom objects allows bypassing role hierarchy inheritance (unchecked = more private)

**Role Hierarchy**
- Managers inherit all subordinate access (read + edit based on OWD)
- Limit to 10 levels of branches; ≤5,000 total roles (Spring '21+ orgs); ≤25,000 internal roles best practice
- Build based on data access needs, NOT org chart — they often diverge

**Sharing Rules**
- **Owner-based**: 300 per object; based on record ownership — for matrix management, overlay scenarios
- **Criteria-based**: 50 per object; based on record field values — for field-driven access (e.g., account region)
- **Guest user**: 50 per object combined with criteria-based; grants access to unauthenticated users — use with extreme caution

**Teams**
- Account teams, Opportunity teams, Case teams — one team per record
- Up to N members with different access levels per team
- If team membership managed externally → integration via API to sync team membership
- Don't use teams if territory management already satisfies the requirement

**Territory Management (Enterprise Territory Management)**
- Matrix hierarchy — sales orgs with two independent reporting lines (role + territory)
- Best for: geographic/segment sales models, overlay sales roles
- Maintain separately from role hierarchy — don't make them identical (causes redundant sharing calculations)
- If territory forecasting AND role forecasting both needed: role hierarchy = HR reporting, territory = sales hierarchy

**Apex Managed Sharing**
- Use when: no declarative option meets needs; external system of truth drives access
- Custom Apex sharing reasons on custom objects — cleaner than manual share row cause
- Performance concern for very large data volumes (>2M accounts)

**Restriction Rules**
- **Narrow** access: filter records user sees even after OWD/sharing grants broader access
- Available for: custom objects, external objects, contracts, events, tasks, time sheets
- ≤2 active rules per object (Enterprise/Developer editions); ≤5 (Performance/Unlimited)
- Applies to: list views, lookups, related lists, reports, search, SOQL, SOSL

**Implicit Sharing**
- Automatic, non-configurable
- Parent: if you can see contact/opportunity/case, you implicitly see the parent account
- Child: account owner gets implicit access to related contacts, opportunities, cases (level set per role)
- Does NOT apply to custom objects

### Performance Gotchas
- **Data skew**: Parent record with 10,000+ children → sharing recalculation performance issues (ratio target: 1:10,000)
- **Ownership skew**: User owning 10,000+ records → put role at top of hierarchy or out of hierarchy entirely
- **Bulk changes**: Defer sharing calculations before mass changes (Salesforce Support required to enable); recalculate once at end
- **Account hierarchy**: Does NOT cascade data access — parent account access ≠ child account access
- **Team + ETM**: Maintain separately; only use teams if territory management can't satisfy the requirement

### Troubleshooting Flow
1. Profile/permission set has object access?
2. OWD allows baseline read?
3. Role hierarchy connects owner and user?
4. Any sharing rule applies?
5. Team membership grants access?
6. ETM territory assignment correct?
7. Manual share exists?
8. Programmatic share created?

## Key Constraints
- OWD changes = full sharing recalculation = potentially hours for large orgs — plan carefully
- Role hierarchy limited to 10 levels of branches deep; exceeding creates performance and maintenance issues
- Public group nesting max 5 levels; total groups ≤100,000
- Restriction rules override all other sharing — test carefully in sandbox before production

## Related Patterns / Alternatives
- [[salesforce-platform]] — Sharing model is the access control layer of the platform architecture
- [[data-360-security-architecture]] — ABAC/CEDAR provides a more dynamic, attribute-based alternative for Data 360 access control

## Dennis's Take
The most common sharing model mistake is starting with too permissive an OWD and then trying to restrict it later. Always design OWD at maximum restriction, then add sharing where needed. For complex matrix sales orgs, territory management is almost always the right answer — don't try to model a matrix in the role hierarchy. And never underestimate the performance impact of sharing recalculation on large orgs.

## Sources
- [[platform-sharing-architecture]] — Complete sharing model reference with use cases, troubleshooting flow, and performance guidance
