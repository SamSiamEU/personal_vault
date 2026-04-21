---
title: Agentic Patterns and Implementation with Agentforce
type: source
format: article
url: raw/Agentic Patterns and Implementation with Agentforce.md
author: Salesforce Architect
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [agentforce, patterns, conversational, proactive, ambient, autonomous, collaborative]
---

# Agentic Patterns and Implementation with Agentforce

## Summary
Comprehensive implementation guide for all five Agentforce agent types with specific CRM use cases, architectural blueprints, and 5 full worked implementation recipes. Covers conversational agents (messaging + email SDR), proactive agents (external and internal event response), ambient agents (stream observer + activity interception), autonomous agents (goal+strategy layer, multi-agent pipeline), and collaborative agents (Slack-based multi-agent swarms). Includes data integration patterns for agents (4 data types), A2A and MCP implementation details, and Agentforce 3.0 platform capabilities.

## Key Takeaways

### Agent Type Patterns
- **Conversational — Interactive Messaging**: Multi-channel (WhatsApp, SMS, Slack, Experience Cloud); Topics/Instructions/Actions/Guardrails/Prompt Templates; Data 360 vector store + RAG; Live Agent escalation with full conversation context
- **Conversational — Email SDR Agent**: Async multi-turn email; BANT qualification; Task/Meeting Scheduling; <5 min first response vs 8–24h for humans; 2-5x SDR capacity increase
- **Proactive — External Event Response**: External system → Pub/Sub API or Data 360 streaming → Flow → Agent Action → notify/act; 24/7 triage
- **Proactive — Internal Salesforce Event Response**: CDC/Platform Events/RTEM → Flow/Apex → Agent Action; intelligent triage beyond rule-based routing
- **Ambient — Stream Observer**: Attaches to video/audio stream; real-time coaching, sentiment analysis, objection handling; window size vs accuracy trade-off
- **Ambient — Activity Interception**: Observes UI actions; surfaces knowledge articles + next-best-actions without prompts; fraud/threat detection
- **Collaborative Pattern**: Shared collaboration surface (Slack); Conversational + Proactive + Ambient agents share data layer tracking episode state across handoffs; human-in-the-loop across teams
- **Autonomous Pattern**: Goal + strategy definition layer with process playbooks, autonomous decision criteria, fallback rules, scopes, success criteria; orchestrator/choreographer agent; three monitoring levels: goal progress / operations / governance

### Agentforce 3.0 Platform
- **Python foundation**: Agentforce 3.0 built on Python; event-driven async framework
- **Multimodal voice**: ASR/TTS integration; WebRTC telephony + gateways; voice agents for phone channel
- **Agentforce Script**: State-machine-based determinism prevents memory loss; conditional handoffs + LLM-determined handoffs; ordered state transitions for complex workflows

### A2A and MCP Implementation
- **A2A**: Agentforce acts as both A2A client and server; Platform Events as durable async transport; "related agents" capability for discovery; MuleSoft connectors to expose Agentforce agents as A2A servers where native A2A not yet supported
- **MCP**: Agentforce as MCP client; MuleSoft as gateway transforming A2A → external MCP calls; AgentExchange for discovering MCP servers

### Data Integration Patterns for Agents
Four data access patterns depending on data type:
1. **External Tools via MCP**: For 3P tools and capabilities; Agentforce as MCP client
2. **Transactional data**: Direct CRUD via MCP for simple operations; complex multi-step → MuleSoft API with SAGA support
3. **Analytical data**: Zero-copy Data 360 query via Calculated Insights API; streaming insights via Data Actions/Apache Flink
4. **Semantic data (RAG)**: Chunking → embedding → Milvus vector store → hybrid search; OR Data Graphs (DMOs + identity resolution + graph traversal via Query API)

### Five Implementation Recipes (Full Step-by-Step)
1. **Service Agent (Conversational)**: Chat → CRM lookup → MuleSoft shipping API → escalation via Omni-Channel
2. **VIP Cart Recovery (Proactive)**: Cart_Abandoned__e Platform Event → Flow → Employee Agent → Data 360 RAG for discount → MC journey enrollment
3. **Discovery Call Assistant (Ambient)**: Zoom RTMS → Amazon Transcribe → Transcript_Segment__e → Flow → Agent → Slack DM
4. **Pipeline Builder (Autonomous)**: Multi-agent: Goal Orchestrator → Research & Qualification Agent → SDR Agent; ZoomInfo via Data 360 connector; AgentGoal__e platform event
5. **Multi-issue Resolution (Collaborative)**: Agentforce Help Agent → MuleSoft Agent Broker → Billing/Logistics/Provisioning specialist agents as A2A servers

## Notable Quotes / Data Points
- Email SDR: "<5 min first response (vs. 8–24 hrs)" and "2-5x increase in lead coverage"
- Ambient stream observer: "high-quality audio = better accuracy BUT more latency — tuning required per use case"
- Collaborative pattern: "a seamless fusion of human and digital labor"
- Pipeline Builder recipe uses Platform Event `AgentGoal__e` as the trigger for autonomous agent activation
- MuleSoft Agent Broker used as routing layer in Multi-issue Resolution — demonstrates MuleSoft as A2A orchestration hub

## Wiki Pages Updated
- [[agentforce]] — Five agent types, Agentforce 3.0, voice, A2A/MCP capabilities, Agentforce Script
- [[agentic-design-patterns]] — All 5 agent type patterns + 5 implementation recipes + data integration patterns
- [[data-360]] — Data 360 as grounding layer (RAG, vector store, Calculated Insights, Data Graph, streaming)
- [[mulesoft]] — MuleSoft as A2A server enabler, MuleSoft Agent Broker in collaborative pattern

## Gaps / Follow-up
- Token expiry and state persistence for long-running autonomous agents (hours/days) not addressed
- Rollback semantics for multi-step autonomous agents across external systems not documented
- Agentforce Script state-machine details (transition syntax, persistence mechanism) not fully covered
