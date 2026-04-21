---
name: MCP and A2A Protocols
type: concept
category: integration-pattern
tags: [mcp, a2a, protocols, agent-interoperability, openstandards]
sources: 3
last_updated: 2026-04-21
---

# MCP and A2A Protocols

## Definition
Open interoperability standards enabling AI agents to communicate with tools (MCP) and with other agents (A2A). Both are fast-evolving open standards that form the communication backbone of multi-agent enterprise architectures.

## When to Use
- **MCP**: When an agent needs to invoke a tool, API, or data source. Use MCP to expose Salesforce capabilities to external agents, or to connect Agentforce agents to external tools (Slack, GitHub, internal databases).
- **A2A**: When multiple agents need to collaborate on a task — especially across different AI platforms or organizational boundaries.

## How It Works

### Model Context Protocol (MCP)
- **Purpose**: Agent-to-tool communication protocol. Defines how agents discover, invoke, and receive results from external tools and data sources
- **Architecture**: Client (agent) connects to MCP server (tool/API wrapper); MCP server exposes a standardized capability manifest
- **Use cases in Salesforce**: 
  - Salesforce Agentforce actions built on MCP servers (expose CRM capabilities to external agents)
  - External agents (built on Claude, GPT, etc.) calling Salesforce data via Salesforce MCP server
  - MuleSoft Anypoint assets exposed as MCP servers (MuleSoft Vibes uses local MCP servers in VSCode/Cursor)
  - Heroku apps publishing MCP servers for custom integrations
- **Enforcement**: MuleSoft Flex Gateway acts as the "Agent Protocol Gateway" — governs all inbound MCP calls with policy enforcement (auth, rate limiting, PII masking)

### Agent2Agent Protocol (A2A)
- **Purpose**: Agent-to-agent communication protocol. Defines how agents advertise capabilities, accept tasks, and return results to orchestrating agents
- **Architecture**: Agent publishes an `agentSpec.yaml` (or similar) advertising its capabilities; orchestrating agent discovers and calls it
- **Use cases in Salesforce**:
  - Agentforce Orchestrator pattern delegates to specialist agents via A2A
  - Multi-vendor scenarios: Salesforce agent calls AWS Bedrock agent or Google Vertex agent via A2A
  - MuleSoft Agent Registry catalogs all A2A-capable agents; Agent Broker routes based on capability matching
- **Trust**: Each agent's identity is cryptographically verified — Trusted Agent Identity in MuleSoft; Einstein Trust Layer in Salesforce

### Combined Architecture
```
User Request
    ↓
Agentforce Orchestrator
    ├── MCP → Tool (CRM data, Slack, GitHub)
    └── A2A → Specialist Agent (Domain SME, external LLM)
              └── MCP → Tool (that specialist's tools)
```

### In the Agentic Enterprise 11-Layer Model
- MCP/A2A operate in the **Agentic Layer** (agent interoperability) and **Integration Layer** (Agent Protocol Gateway)
- They are the mechanism for the Agentic Layer's "Agent Interoperability Protocols" capability
- Governed by the **Enterprise Orchestration Layer** (blended model: local choreography via MCP/A2A + centralized oversight via orchestrator)

## Key Constraints
- Both protocols are still maturing (2024-2025 standard period); vendor implementations may not be fully interoperable
- MCP server security: SSRF risk if MCP servers are not properly sandboxed — external MCP calls can be vectors for prompt injection
- A2A calls add latency to agent reasoning chains; orchestration depth matters for response time SLAs
- Identity propagation must be explicitly designed: agent-to-agent calls need OBO or S2S tokens to maintain user context

## Related Patterns / Alternatives
- [[mulesoft-agent-fabric]] — MuleSoft's implementation of the governance layer for MCP/A2A
- [[identity-propagation-patterns]] — How end-user identity flows through MCP/A2A call chains
- [[agent-orchestration-archetypes]] — SOMA/MOMA/Multi-Vendor A2A use MCP/A2A as their communication mechanism

## Dennis's Take
MCP is the practical choice right now — you can build MCP servers for existing APIs quickly, and both Salesforce and MuleSoft have tooling for it. A2A is more powerful but more complex; don't design multi-vendor A2A architectures until you have a mature agent governance layer (i.e., MuleSoft Agent Fabric) in place.

## Sources
- [[architecting-agentic-enterprise-mulesoft]] — MCP/A2A as Vibes AI tooling; Flex Gateway as protocol gateway
- [[enterprise-agentic-architecture-design-patterns]] — MCP/A2A in the context of SOMA/MOMA archetypes
- [[agentic-enterprise-it-architecture]] — MCP/A2A as the Agent Interoperability Protocols capability in the 11-layer model
