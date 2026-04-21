---
name: MuleSoft
type: entity
category: integration-tool
tags: [mulesoft, integration, api-led, anypoint, agent-fabric]
sources: 4
last_updated: 2026-04-21
---

# MuleSoft

## What It Is
MuleSoft is Salesforce's integration platform, built around the Anypoint Platform. It enables organizations to connect applications, data, and devices across on-premises and cloud environments through API-led connectivity. In the agentic era, MuleSoft has evolved to serve as the integration and orchestration layer for AI agent ecosystems via MuleSoft Agent Fabric.

## Relevance to Architecture Work
MuleSoft is the go-to platform for enterprise integration patterns, API management, and — increasingly — multi-agent orchestration. Architects use it for: event-driven integration, real-time API mediation, B2B/EDI, and governing AI agent interactions across heterogeneous platforms (Salesforce, AWS Bedrock, Google Vertex, legacy systems). It's the connective tissue between Salesforce and the broader enterprise.

## Key Capabilities
- **API-led Connectivity**: System/Process/Experience API hierarchy — the foundational integration philosophy
- **Anypoint Platform**: Runtime manager, API manager, Exchange (reusable asset catalog), Flex Gateway
- **CloudHub 2.0**: Fully managed cloud deployment target on AWS; multi-AZ within a region, no native multi-region HA
- **Agent Fabric**: Four pillars for multi-agent governance — Discover, Orchestrate, Govern, Observe
- **Agent Registry**: Catalog of all A2A agents and MCP servers across the ecosystem (including Informatica, Bedrock, Vertex)
- **Agent Broker**: Dynamic routing engine that matches tasks to the right agent or tool
- **Flex Gateway**: Policy enforcement at outbound API calls — where identity propagation (OBO, S2S) and agent governance rules are enforced
- **Agent Visualizer**: Real-time observability of agent reasoning chains and inter-agent communication
- **MuleSoft Vibes**: AI dev tools — generate APIs, integrations, and tests from natural language prompts; supports MCP local servers in VSCode/Cursor
- **Trusted Agent Identity**: Cryptographic identity for agents; enables OBO token exchange (RFC 8693) and S2S for agent-to-API calls
- **OTEL observability**: OpenTelemetry integration for distributed tracing of agent and API calls
- **B2B / EDI**: Partner management and EDI compliance for supply chain integrations
- **Anypoint Code Builder (ACB)**: Next-gen IDE with built-in MCP server; AI-generated integrations from natural language; Topic Center creates Agentforce-invocable actions from Anypoint Exchange assets
- **Integration Intelligence**: Next-gen observability layer built on Data 360 + Tableau Semantics + Tableau Next — operational insights beyond OTEL
- **Bidirectional MCP**: Salesforce/MuleSoft as MCP client (consuming external tools) AND MCP server (exposing Anypoint capabilities to agents)
- **A2A and Inference Connectors**: Native connectors for A2A protocol and AI model inference endpoints
- **Interpreted Connectivity**: Low/no-code integration layer for non-technical builders
- **RPA and IDP**: Robotic Process Automation and Intelligent Document Processing for legacy system and document integration

## Licensing / Pricing
Anypoint Platform has capacity-based pricing (vCores for CloudHub, API calls for flex gateway). Agent Fabric capabilities are additive. Exact pricing requires Salesforce contract review.

## Strengths
- Best platform for real-time API mediation, orchestration, and transactional reliability in short-lived processes
- Agent Fabric is the most mature cross-vendor agent governance framework in the Salesforce ecosystem
- Out-of-the-box compliance certifications: FedRAMP, ISMAP, HITRUST, SOC 1/2/3, ISO 27001
- 300+ connectors supporting all integration styles (ETL, ELT, Reverse ETL, streaming)

## Weaknesses / Gaps
- CloudHub 2.0 has no native multi-region HA — requires active-active/warm standby architecture with AWS Route 53
- Not designed for bulk data management or MDM — that's Informatica's domain
- Object Store V2 is region-bound — cross-region DR requires externalizing state

## Known Gotchas
- Object Store V2 stays tied to the region where an app was first deployed — moving regions doesn't migrate Object Store data
- US East region is the control plane for Anypoint Platform; a US East outage makes Runtime Manager unavailable even for apps in other regions
- Private space setup is regional; must be pre-configured in DR region before disaster strikes

## Contradictions / Open Questions
- How Agent Fabric interoperates with non-Salesforce orchestrators (e.g., AWS Bedrock Agent Orchestrator) under a unified governance model is still evolving

## Sources
- [[architecting-agentic-enterprise-mulesoft]] — Agent Fabric deep-dive, governance policies, OTEL observability
- [[mulesoft-agent-fabric-deep-dive]] — 4 pillars, Agent Registry/Broker, Conway's Law vs DDD for hierarchy design
- [[end-user-identity-propagation-agents]] — Trusted Agent Identity, OBO/S2S patterns enforced at Flex Gateway
- [[cloudhub-20-ha-dr]] — CloudHub 2.0 HA/DR architecture, active-active/warm/cold standby options
- [[leveraging-mulesoft-informatica]] — MuleSoft vs Informatica positioning, "Better Together" framework
- [[salesforce-platform-transformed-tomorrow]] — Anypoint Code Builder, Integration Intelligence, bidirectional MCP, A2A/Inference Connectors, RPA/IDP
- [[agentic-patterns-agentforce]] — MuleSoft as A2A orchestration hub (Multi-issue Resolution recipe), MuleSoft Agent Broker in collaborative patterns
