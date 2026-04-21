---
name: Agent Orchestration Archetypes
type: concept
category: architecture-pattern
tags: [orchestration, multi-agent, a2a, mulesoft, agentforce, soma, moma]
sources: 2
last_updated: 2026-04-21
---

# Agent Orchestration Archetypes

## Definition
System-level orchestration patterns that define how multiple agents, human workers, and deterministic systems are coordinated to accomplish complex enterprise workflows. Four archetypes cover the spectrum from single-orchestrator to multi-vendor multi-agent architectures.

## When to Use
Use these archetypes to design the overall agent coordination topology before choosing individual agent patterns. The archetype determines where the orchestration intelligence lives (Salesforce vs. MuleSoft), how cross-cloud agent calls are routed, and how governance is applied.

## How It Works

### Four Orchestration Archetypes

#### 1. SOMA — Single Orchestrator, Multi-Agent
- **Structure**: One Salesforce Agentforce orchestrator; delegates to multiple specialist agents within Salesforce
- **When to use**: All agent capabilities within the Salesforce ecosystem; no external AI platforms
- **Key mechanism**: Orchestrator pattern (from [[agentic-design-patterns]]) decomposes goals and routes to Domain SME agents
- **Governance**: Managed within Salesforce Einstein Trust Layer and Agentforce guardrails

#### 2. MOMA — Multi-Orchestrator, Multi-Agent
- **Structure**: Multiple orchestrators (one per domain/team); each manages its own specialist agents; inter-orchestrator coordination at the top level
- **When to use**: Large enterprises with distinct business domains (Sales, Service, Supply Chain) that each have their own agent ecosystems needing governance separation
- **Key mechanism**: Conway's Law alignment — teams own their orchestrators; domain-driven design for agent boundaries
- **Governance**: Each orchestrator enforces its own policies; cross-domain calls use A2A with identity propagation

#### 3. Multi-Vendor A2A — Salesforce-Led
- **Structure**: Agentforce as the primary orchestrator; extends to external AI agents (AWS Bedrock, Google Vertex, custom LLMs) via A2A protocol and MCP
- **When to use**: Salesforce is the system of engagement; external AI platforms are specialist workers
- **Key mechanism**: Agentforce initiates A2A calls to external agents; MCP servers expose external tools to Salesforce agents
- **Governance**: Einstein Trust Layer + Agentforce guardrails as primary governance layer; external agent responses validated at Trust Layer boundary

#### 4. Multi-Vendor A2A — MuleSoft-Led
- **Structure**: MuleSoft Agent Fabric as the central governance and routing layer; Salesforce Agentforce and all other AI platforms are worker agents behind the fabric
- **When to use**: Enterprise already uses MuleSoft as integration backbone; heterogeneous AI landscape (Salesforce, Bedrock, Vertex, on-prem models); need cross-vendor governance, observability, and identity enforcement
- **Key mechanism**: Agent Broker routes tasks; Flex Gateway enforces identity (OBO/S2S); Agent Visualizer provides end-to-end observability; Agent Registry catalogs all agents regardless of vendor
- **Governance**: Single governance plane (Anypoint) covers all agent calls across all vendors

### Choosing Between Archetypes
| Factor | SOMA | MOMA | Salesforce-Led A2A | MuleSoft-Led A2A |
|--------|------|------|-------------------|-----------------|
| Ecosystem | Salesforce-only | Multi-domain Salesforce | Salesforce + external AI | Heterogeneous |
| Governance complexity | Low | Medium | Medium | High |
| Existing MuleSoft investment | Not needed | Optional | Optional | Required |
| Cross-domain coordination | Flat | Hierarchical | External-facing | Full enterprise |

## Key Constraints
- MuleSoft-Led A2A requires Agent Fabric to be provisioned and Agent Registry populated before cross-vendor governance works
- A2A protocol is still maturing — vendor-specific implementations may diverge
- Identity propagation across orchestrators requires explicit design (OBO tokens expire; S2S has different trust model)

## Related Patterns / Alternatives
- [[agentic-design-patterns]] — Individual agent patterns that operate within these archetypes
- [[mcp-a2a-protocols]] — The underlying protocols enabling cross-system agent communication
- [[mulesoft-agent-fabric]] — The MuleSoft implementation enabling the MuleSoft-Led A2A archetype
- [[identity-propagation-patterns]] — How agent identity flows across orchestrators and API calls

## Dennis's Take
Start with SOMA unless you have explicit cross-cloud requirements. MOMA is right for large enterprises with distinct IT domains. The MuleSoft-Led A2A archetype gives maximum governance but requires significant MuleSoft maturity — don't attempt it without a mature Anypoint implementation already in place.

## Sources
- [[enterprise-agentic-architecture-design-patterns]] — Four archetypes defined and compared
- [[architecting-agentic-enterprise-mulesoft]] — MuleSoft-Led archetype deep-dive, governance policies table
