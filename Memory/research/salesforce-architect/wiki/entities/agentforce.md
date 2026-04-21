---
name: Agentforce
type: entity
category: salesforce-cloud
tags: [agentforce, ai-agents, atlas, einstein, salesforce]
sources: 6
last_updated: 2026-04-21
---

# Agentforce

## What It Is
Agentforce is Salesforce's native AI agent platform, launched at Dreamforce 2024. It enables organizations to build, deploy, and manage autonomous AI agents directly within the Salesforce Platform. Agents reason over CRM data and enterprise knowledge to take goal-oriented actions across sales, service, marketing, and commerce workflows — without requiring direct user prompts for each step.

## Relevance to Architecture Work
Agentforce is the primary vehicle for deploying AI agents on Salesforce. Every agentic architecture decision on the platform — conversational vs. proactive vs. ambient vs. autonomous — runs through Agentforce. Architects must understand topics/actions/guardrails/prompt templates as the four core agent configuration primitives, and how agents connect to Data 360, Flow, and Apex.

## Key Capabilities
- **Five agent types**: Conversational (reactive NL dialog), Proactive (event-triggered), Ambient (background observers), Autonomous (goal-directed multi-step), Collaborative (swarm/A2A)
- **Topics and instructions**: Define agent persona, mission, and scope of authorized actions
- **Actions**: Executable tools built on Flow, Apex, or external MCP servers
- **Guardrails**: Runtime safety layer — intercepts prompts, validates actions, filters responses
- **Prompt templates**: Reusable templates populated dynamically with CRM/Data 360 context via merge fields or RAG
- **Einstein Trust Layer**: PII masking, zero-data-retention for LLM calls, toxic content detection
- **Atlas Reasoning Engine**: LLM-based planner that decomposes goals into action sequences
- **Agentforce DX + Python SDK**: Dev tooling for local testing, `agentSpec.yaml` for agent definitions
- **STDM (Session Tracing Data Model)**: Observability framework — logs every step, action, and decision in audit trail
- **Agentforce Optimization/Moments**: Continuous improvement tooling for agent performance
- **Agentforce 3.0**: Python foundation; event-driven async framework; multimodal voice (ASR/TTS/WebRTC telephony + gateways); Agentforce Script (state-machine determinism, prevents memory loss, conditional/LLM-determined handoffs)
- **A2A Server capability**: Agentforce acts as both A2A client (calling other agents) and A2A server (receiving task assignments); Platform Events as durable async transport; "related agents" for capability discovery
- **MCP Client**: Agentforce as MCP client; uses MuleSoft as gateway to transform A2A → external MCP calls; AgentExchange for MCP server discovery
- **Platform layers**: AI Platform → AI Foundational Services (AI Gateway/Feedback/RAG/Agentic Orchestration/Agent Evaluation) → Agentforce Studio (Agent Builder/Prompt Builder/Testing Center/Model Builder/Next Gen Authoring)

## Licensing / Pricing
Consumption-based model (conversations/actions). Exact rates depend on Salesforce contract and edition. Agent credits are separate from standard Salesforce licenses.

## Strengths
- Native platform integration — agents have direct access to CRM data, Flows, Apex without custom connectors
- Einstein Trust Layer provides enterprise-grade data governance for LLM calls
- Multi-channel support (WhatsApp, SMS, email, Experience Cloud, Slack)
- Works with MuleSoft Agent Fabric for cross-cloud agent orchestration via A2A and MCP

## Weaknesses / Gaps
- Complex agents require significant topic/action tuning — harder to configure than traditional automation
- Performance and accuracy depend heavily on Data 360 data quality and RAG vector store curation
- Governance tooling (STDM, Agentforce Optimization) is maturing — still early for enterprise-scale observability
- A2A protocol and multi-vendor agent orchestration is still emerging

## Known Gotchas
- Governor limits still apply to Apex-based agent actions — same bulkification concerns as standard Apex
- Async agent execution introduces eventual consistency — agents cannot atomically roll back cross-system actions
- Identity propagation to downstream systems (MuleSoft APIs, external tools) requires explicit OBO or S2S token patterns — not automatic

## Contradictions / Open Questions
- Exact boundary between Atlas Reasoning Engine internal planning and user-defined topics/instructions is not fully documented
- How Agentforce handles agent version management during production changes is unclear

## Sources
- [[agentic-patterns-agentforce]] — All 5 agent types + 5 implementation recipes + Agentforce 3.0 + A2A/MCP implementation + data integration patterns
- [[enterprise-agentic-architecture-design-patterns]] — 15 architectural patterns and 4 orchestration archetypes
- [[agent-development-lifecycle]] — ADLC 5 phases, DX tooling, STDM, Agentforce Optimization
- [[end-user-identity-propagation-agents]] — identity propagation from Agentforce to downstream systems
- [[data-360-architecture]] — Data 360 as Agentforce's data foundation (DMOs, vector store, RAG)
- [[agentic-enterprise-it-architecture]] — Agentforce positioning in 11-layer agentic IT architecture
- [[salesforce-platform-transformed-tomorrow]] — Agentforce platform layers (AI Foundational Services, Studio), Agentforce 3.0 voice/Python, Customer Zero
