---
title: Enterprise Agentic Architecture and Design Patterns
type: source
format: article
url: raw/Enterprise Agentic Architecture and Design Patterns.md
author: Salesforce Architect
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [agentforce, design-patterns, orchestration, archetypes, multi-agent]
---

# Enterprise Agentic Architecture and Design Patterns

## Summary
Comprehensive catalog of 15 named agent patterns and 4 orchestration archetypes for Salesforce agentic implementations. Defines the taxonomy of agent types (Greeter through Project Manager) and maps out the four system-level orchestration models (SOMA, MOMA, Multi-Vendor A2A Salesforce-led, Multi-Vendor A2A MuleSoft-led). The primary reference for agentic architecture pattern selection on Salesforce.

## Key Takeaways
- 15 named patterns cover the full spectrum from simple routing (Greeter) to complex governance (Judge & Jury) to swarm intelligence (Model of Models)
- Orchestrator pattern remains the front-door and aggregates results — different from Operator which routes to specialist agents
- SOMA: simplest single-orchestrator pattern for Salesforce-only ecosystems
- MOMA: multi-orchestrator for large enterprise with distinct BU agent ecosystems
- Multi-Vendor A2A (Salesforce-led): Agentforce orchestrates external AI agents via A2A/MCP
- Multi-Vendor A2A (MuleSoft-led): MuleSoft Agent Fabric as governance layer; all AI vendors (incl. Salesforce) are workers
- Pattern library is a living document — Project Manager pattern implied but not formally numbered

## Notable Quotes / Data Points
- "Choosing the right [archetype] determines where orchestration intelligence lives, how cross-cloud agent calls are routed, and how governance is applied"
- 4 archetypes span: ecosystem complexity (Salesforce-only → multi-vendor), governance complexity (low → high), MuleSoft dependency (none → required)

## Wiki Pages Updated
- [[agentic-design-patterns]] — All 15 named patterns
- [[agent-orchestration-archetypes]] — All 4 archetypes with selection criteria

## Gaps / Follow-up
- Specific implementation blueprints for each pattern not fully covered — follow-up with pattern-specific reference docs if available
- How patterns evolve with Agentforce product roadmap needs monitoring
