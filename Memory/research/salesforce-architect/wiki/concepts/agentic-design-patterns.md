---
name: Agentic Design Patterns
type: concept
category: architecture-pattern
tags: [agents, agentforce, patterns, orchestration, agentic]
sources: 3
last_updated: 2026-04-21
---

# Agentic Design Patterns

## Definition
Reusable architectural blueprints for building AI agents on the Salesforce platform. Patterns address specific use cases for each of the five agent types (Conversational, Proactive, Ambient, Autonomous, Collaborative) and 15 named agent archetypes.

## When to Use
Use these patterns as starting points when scoping an Agentforce implementation. Match the business requirement to an agent type first, then select the specific named pattern that best fits the use case.

## How It Works

### Five Agent Types
| Type | Trigger | Primary Use Case |
|------|---------|-----------------|
| **Conversational** | User prompt (NL dialog) | Customer service, SDR lead qualification, multi-channel engagement |
| **Proactive** | Event / data change | SLA breach prevention, order status updates, external system signals |
| **Ambient** | Background observation (stream/UI) | Call coaching, activity capture, real-time sales guidance |
| **Autonomous** | High-level goal | Lead generation campaigns, complex multi-step workflows |
| **Collaborative** | Decomposed task from orchestrator | Agent swarms — each specialist handles one domain |

### 15 Named Agent Patterns (from Enterprise Agentic Architecture)
1. **Greeter** — NL intent understanding → route to human or agent
2. **Operator** — Extends Greeter; routes to specialist AI agent or human; negotiates intent
3. **Orchestrator** — Manages agent swarm; decomposes requests, delegates, aggregates; stays front-door
4. **Listener/Feed** — Subscribes to data/event streams; surfaces relevant context
5. **Workspace** — Persistent collaborative environment for human+agent co-work
6. **Answerbot** — Self-service knowledge retrieval via generative AI (not just keyword match)
7. **Domain SME** — Deep expertise in one domain; invoked by Orchestrator
8. **Interrogator** — Assembles context from multiple sources to answer complex questions
9. **Prioritizer** — Ranks and routes work items based on business rules + AI judgment
10. **Generator** — Creates structured content (emails, summaries, proposals, code)
11. **Data Steward** — Monitors data quality; enriches/corrects records autonomously
12. **Zen Gardener** — Scheduled data grooming: deduplication, standardization, archival
13. **Configurer** — Makes platform/system configuration changes based on instructions
14. **Judge & Jury** — Multi-juror agent for evaluating outputs; judge aggregates verdicts
15. **Model of Models** — Aggregates diverse expert agent viewpoints for richer insights
16. **Project Manager** — Coordinates complex multi-step human+agent work (implied 16th)

### Key Conversational Patterns
- **Interactive Messaging Agent**: Multi-channel (WhatsApp, SMS, Slack, Experience Cloud); uses RAG from Data 360 vector store; routes to Live Agent when unresolved
- **Interactive Email SDR Agent**: Async lead qualification; schedules meetings; updates CRM; handles BANT collection over email threads

### Key Proactive Patterns
- **External Event Response**: External system → Pub/Sub API or Data 360 ingestion → Flow → Agent Action → notify/act
- **Internal Salesforce Event Response**: CDC/Platform Events/RTEM → Flow/Apex → Agent Action → notify/act

### Key Ambient Patterns
- **Stream Observer (Call Coaching)**: Attaches to video/audio stream; real-time coaching, sentiment analysis, objection handling
- **Activity Interception**: Observes UI actions; surfaces knowledge articles, next-best-actions without user prompting

### Collaborative Pattern
- Human-in-the-loop model: Conversational agent initiates → Proactive agent handles backend → Ambient agent provides guidance
- Multi-team collaboration where different specialists (internal + external) hand off via A2A protocols

## Key Constraints
- All Apex-based agent actions subject to Salesforce governor limits (callouts, DML, SOQL)
- Async agent execution means no atomic cross-system rollback — compensating transactions must be designed explicitly
- Guardrails add latency; complex guardrail evaluation chains can affect response time
- Real-time ambient patterns (stream observer) require low-window sizes for latency — trade-off with accuracy

## Related Patterns / Alternatives
- [[agent-orchestration-archetypes]] — SOMA/MOMA/Multi-Vendor A2A are the system-level orchestration patterns that these agent patterns operate within
- [[mcp-a2a-protocols]] — Protocols that enable agent-to-tool and agent-to-agent communication
- [[async-processing-patterns]] — When agent actions need to trigger async workloads (Batch Apex, Platform Events)

## Dennis's Take
The Greeter → Operator → Orchestrator hierarchy is a good default starting architecture for most Salesforce agentic implementations. Start with the Greeter, prove intent resolution works, then add specialist agents as the Operator routes to them. Don't try to build the full Orchestrator pattern on day one.

## Contradictions / Open Questions
- The "Project Manager" pattern is implied but not formally listed in the 15 — may be in development
- How "Judge & Jury" integrates with Einstein Trust Layer guardrails is not fully specified

## Sources
- [[enterprise-agentic-architecture-design-patterns]] — 15 named patterns, 4 archetypes
- [[agentic-patterns-agentforce]] — Conversational, proactive, ambient, collaborative agent recipes with implementation details
- [[agent-development-lifecycle]] — How to build and test agents using ADLC + DX tooling
