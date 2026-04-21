---
title: MuleSoft Agent Fabric — Deep Dive
type: source
format: article
url: raw/MuleSoft Agent Fabric - Deep Dive.md
author: MuleSoft/Salesforce
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [mulesoft, agent-fabric, registry, broker, flex-gateway, visualizer, governance]
---

# MuleSoft Agent Fabric — Deep Dive

## Summary
Technical deep-dive into MuleSoft Agent Fabric's four pillars: Discover (Agent Registry/Exchange), Orchestrate (Agent Broker/YAML spec), Govern (Flex Gateway policies), and Observe (Agent Visualizer/OTEL). Covers hierarchical agent network design patterns using Conway's Law alignment vs. Domain-Driven Design. The most detailed technical reference for Agent Fabric architecture.

## Key Takeaways
- **Discover**: Agent Registry uses built-in scanners to auto-catalog every A2A agent and MCP server (incl. Informatica, Bedrock, Vertex); no manual registration needed
- **Orchestrate**: Agent Broker dynamically routes to correct agent/tool using YAML capability spec; eliminates manual handoffs
- **Govern**: Three enforcement levels — end-to-end interactions (OBO/S2S), model layer (LLM requests), execution layer (action controls)
- **Observe**: Agent Visualizer shows complete agent call graph in real time; OTEL distributed traces; anomaly detection; semantic observability (business context enrichment)
- **Hierarchy design**: Conway's Law = mirror org chart (clear ownership, stable boundaries); DDD = mirror business capabilities (better for cross-functional); use DDD for design, Conway's for ownership governance
- Agent Fabric requires Flex Gateway to be deployed as prerequisite
- `agentSpec.yaml` is the standard for agent capability publishing — not all vendors publish compliant specs yet

## Notable Quotes / Data Points
- Four pillars map directly to governance challenges: shadow agents (Discover), coordination gaps (Orchestrate), compliance risk (Govern), debugging opacity (Observe)
- "MuleSoft Agent Fabric provides a systematic, four-pillar framework" — also mentioned in Leveraging MuleSoft and Informatica source

## Wiki Pages Updated
- [[mulesoft-agent-fabric]] — Four pillars, hierarchy design approaches, Flex Gateway enforcement
- [[mulesoft]] — Agent Fabric as core MuleSoft capability
- [[identity-propagation-patterns]] — Govern pillar's three enforcement levels

## Gaps / Follow-up
- agentSpec.yaml format not fully reproduced — worth extracting for reference when building agents
- Agent Visualizer UI capabilities vs. OTEL traces — what's inspectable in GUI vs. needs custom query
