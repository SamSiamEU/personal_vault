---
name: MuleSoft Agent Fabric
type: concept
category: architecture-pattern
tags: [mulesoft, agent-fabric, governance, orchestration, observability, multi-agent]
sources: 2
last_updated: 2026-04-21
---

# MuleSoft Agent Fabric

## Definition
A four-pillar governance and orchestration framework built on MuleSoft Anypoint Platform that enables enterprises to manage heterogeneous multi-agent ecosystems. Agent Fabric provides the control plane for discovering, orchestrating, governing, and observing AI agents regardless of vendor origin.

## When to Use
- When managing agents from multiple vendors (Salesforce Agentforce, AWS Bedrock, Google Vertex, custom models)
- When enterprise-wide governance (identity, policy, compliance) must apply uniformly across agent calls
- When building the MuleSoft-Led Multi-Vendor A2A orchestration archetype (see [[agent-orchestration-archetypes]])

## How It Works

### Four Pillars

#### 1. Discover
- **Components**: Agent Registry, Exchange (MuleSoft's existing asset catalog)
- **Function**: Automatically catalogs and synchronizes every A2A agent and MCP server in the ecosystem
  - Covers Salesforce agents, Informatica data agents, AWS Bedrock agents, Google Vertex agents, and custom agents
  - Built-in scanners detect new agents and update the registry without manual configuration
- **Value**: Enables instant discovery and reuse; eliminates shadow agents and rogue AI deployments

#### 2. Orchestrate
- **Components**: Agent Broker, `agentSpec.yaml` YAML specification
- **Function**: Receives orchestration requests and dynamically routes tasks to the correct agent or tool
  - Agent Broker matches task requirements against registered agent capabilities
  - Eliminates manual handoffs between agents
  - Transforms scattered individual agents into a coordinated workforce
- **YAML spec**: Each agent publishes an `agentSpec.yaml` that describes its capabilities, inputs, outputs, and constraints

#### 3. Govern
- **Components**: Flex Gateway, Trusted Agent Identity
- **Function**: Policy-driven security and compliance at three enforcement levels:
  1. **End-to-end interactions**: OBO/S2S/In-Task identity propagation for all agent calls (see [[identity-propagation-patterns]])
  2. **Model layer**: LLM request governance (PII masking, rate limiting, content policies on LLM calls)
  3. **Execution layer**: Action-level controls (what tools an agent can call, what data it can access)
- **Declarative policies**: Defined as code; applied consistently across all agent interactions

#### 4. Observe
- **Components**: Agent Visualizer, centralized monitoring (OpenTelemetry)
- **Function**: Real-time visibility into agent reasoning, performance, and collaboration
  - Agent Visualizer shows full agent call graph — which agents called what, in what order, with what outcome
  - OTEL tracing provides distributed traces across agent chains and API calls
  - Anomaly detection: deviations from established reasoning patterns trigger alerts
  - Semantic Observability: connects telemetry to business context (not just technical metrics)

### Agent Network Design — Conway's Law vs. Domain-Driven Design
Two approaches for designing hierarchical agent networks:

| Approach | Description | When to Use |
|----------|-------------|-------------|
| **Conway's Law** | Agent hierarchy mirrors org structure; teams own their agents | Large enterprises with stable org boundaries; clear team ownership |
| **Domain-Driven Design** | Agent hierarchy based on business domain capabilities | Complex domains that don't align with org chart; cross-functional workflows |

Recommendation: Use DDD for capability design, then assign Conway's Law ownership for governance. Don't let org chart dictate agent capabilities.

## Key Constraints
- Agent Fabric requires Agent Registry to be populated before governance kicks in — bootstrapping takes effort
- `agentSpec.yaml` standardization is needed for all agents in the fabric; external vendors may not publish compliant specs
- Flex Gateway deployment must precede Agent Fabric rollout — it is the enforcement point
- Observe pillar (OTEL) generates high telemetry volume — storage and processing costs scale with agent call volume

## Related Patterns / Alternatives
- [[agent-orchestration-archetypes]] — Agent Fabric enables the MuleSoft-Led Multi-Vendor A2A archetype
- [[mcp-a2a-protocols]] — Agent Fabric governs MCP and A2A calls but doesn't replace them
- [[identity-propagation-patterns]] — Govern pillar implements OBO/S2S/In-Task via Flex Gateway

## Dennis's Take
Agent Fabric is the right governance layer for enterprises with significant non-Salesforce AI investments. If you're running Salesforce-only agents, stick with Einstein Trust Layer + Agentforce guardrails. Bring in Agent Fabric when you need to govern agents across vendors — particularly when compliance teams demand a single audit trail.

## Sources
- [[mulesoft-agent-fabric-deep-dive]] — Four pillars in depth, Agent Registry/Broker/Visualizer, hierarchy design approaches
- [[architecting-agentic-enterprise-mulesoft]] — Agent Fabric in context of full MuleSoft agentic architecture
