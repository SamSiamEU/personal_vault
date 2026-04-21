---
title: End-User Identity Propagation in Agents
type: source
format: article
url: raw/End-User Identity Propagation in Agents.md
author: MuleSoft/Salesforce
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [identity, security, obo, s2s, agents, flex-gateway, rfc-8693]
---

# End-User Identity Propagation in Agents

## Summary
Technical specification for how end-user identity (or service identity) is carried through multi-hop agent call chains in MuleSoft. Defines three patterns — OBO (On-Behalf-Of via RFC 8693 token exchange), S2S (server-to-server via client credentials), and In-Task Authorization Code (cross-domain challenge-response) — all enforced at the Flex Gateway outbound policy layer.

## Key Takeaways
- OBO: user JWT exchanged for downstream-scoped token at Flex Gateway; user's permissions enforced at downstream API; RFC 8693 standard
- S2S: agent uses its own client credentials; service identity only; appropriate for non-user-specific data
- In-Task AuthCode: agent encounters 401 challenge mid-task from cross-domain resource; escalates for human authorization or cross-domain OAuth; most complex pattern
- All three patterns are Flex Gateway outbound policies — not baked into Agentforce itself
- Without explicit identity propagation, agent calls use service account identity — may be over/under-privileged
- OBO tokens expire — long-running agent workflows need token refresh logic

## Notable Quotes / Data Points
- "Trusted Agent Identity" is MuleSoft's branding for the overall identity framework
- Flex Gateway is the sole enforcement point — must be deployed and configured before any identity propagation works

## Wiki Pages Updated
- [[identity-propagation-patterns]] — Full specification of all three patterns
- [[mulesoft-agent-fabric]] — Govern pillar identity enforcement
- [[mulesoft]] — Trusted Agent Identity capability

## Gaps / Follow-up
- How identity propagation works for Salesforce Agentforce-native agent calls (without MuleSoft) is not covered — research Agentforce's own identity model
- Token refresh mechanics for long-running agent workflows not fully specified
