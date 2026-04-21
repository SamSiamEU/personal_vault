---
name: Agent Development Lifecycle (ADLC)
type: concept
category: devops-pattern
tags: [adlc, agentforce, dx, sdlc, lifecycle, testing]
sources: 1
last_updated: 2026-04-21
---

# Agent Development Lifecycle (ADLC)

## Definition
A five-phase framework for building, testing, deploying, and improving AI agents — analogous to the SDLC for traditional software but adapted for the non-deterministic, probabilistic nature of AI agents.

## When to Use
Use ADLC to structure any Agentforce agent project, from initial scoping through ongoing monitoring. The framework helps teams avoid the most common failure modes (topic misclassification, hallucination, over-reliance on human escalation) by building evaluation criteria and observability into the process from the start.

## How It Works

### Five Phases

#### Phase 1: Ideation
- Define agent scope: what business problem, what channels, what human-in-the-loop touchpoints
- Map out agent type (conversational/proactive/ambient/autonomous/collaborative — see [[agentic-design-patterns]])
- Identify data requirements: what DMOs, knowledge articles, and RAG sources the agent needs
- Output: Agent specification doc / product requirements

#### Phase 2: Development
- **Agentforce DX**: CLI-based local development environment for defining agents outside the UI
- **agentSpec.yaml**: Declarative YAML that defines agent topics, actions, guardrails, and prompt templates
- **Python SDK**: Testing agents programmatically; useful for CI/CD integration
- Build agent components: topics and instructions, actions (Flow/Apex/external MCP), guardrails, prompt templates
- Configure Data 360 RAG retrievers and vector store for knowledge grounding

#### Phase 3: Testing
- **STDM (Session Tracing Data Model)**: Captures every step, action, and LLM call in a structured audit trail during testing
- **Test failure categories** (common):
  - Topic misclassification: agent routes to wrong topic
  - Hallucination: agent invents facts not in grounded knowledge
  - Action failure: tool call errors (governor limits, API timeouts)
  - Guardrail false positives: blocking legitimate requests
  - Escalation over-reliance: escalating to human when agent could have resolved
- Test with diverse inputs, including adversarial prompts and edge cases
- Python SDK enables programmatic test suites with assertions on agent outputs

#### Phase 4: Deployment
- Deploy via SFDX/Salesforce DX release pipeline (metadata deployments)
- `agentSpec.yaml` included in deployment package for version control
- Staging → UAT → Production promotion with CI/CD hooks
- Configuration via named credentials for API connections, encrypted secrets

#### Phase 5: Monitoring and Tuning
- **Agentforce Optimization**: Built-in tools for identifying where agents fail in production
- **Agentforce Moments**: Specific interaction instances flagged for human review and improvement
- **STDM in production**: Ongoing audit trail for compliance and debugging
- **Closed feedback loop**: Production telemetry → prompt adjustment → new deployment → improved accuracy
- KPIs: containment rate (% resolved without escalation), CSAT, action success rate, latency per topic

## Key Constraints
- STDM generates significant log data at scale — storage governance needed for high-volume deployments
- Python SDK test coverage doesn't guarantee production accuracy — LLM non-determinism means edge cases always emerge in production
- Guardrail tuning is iterative — too tight → false positives → poor UX; too loose → safety risk
- `agentSpec.yaml` is still a relatively new format; version control and conflict resolution practices are maturing

## Related Patterns / Alternatives
- [[agentic-design-patterns]] — Defines what agent types and patterns ADLC applies to
- [[async-processing-patterns]] — When agent actions trigger async workloads, testing must cover failure/retry scenarios
- [[mcp-a2a-protocols]] — Agents using MCP/A2A need additional test coverage for protocol interactions

## Dennis's Take
Invest heavily in Phase 5 infrastructure from day one — most agent teams underestimate ongoing tuning cost. STDM-based observability is essential; build dashboards for containment rate and topic distribution in the first sprint. Use Agentforce Moments as a systematic improvement process, not an ad-hoc review.

## Sources
- [[agent-development-lifecycle]] — ADLC 5 phases, DX tooling, agentSpec.yaml, STDM, Agentforce Optimization/Moments, failure categories
