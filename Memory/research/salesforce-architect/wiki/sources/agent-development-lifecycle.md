---
title: The Agent Development Lifecycle From Conception to Production
type: source
format: article
url: raw/The Agent Development Lifecycle From Conception to Production.md
author: Salesforce Architect
date_published: 2025-01-01
date_ingested: 2026-04-21
tags: [adlc, agentforce, dx, testing, stdm, monitoring]
---

# The Agent Development Lifecycle From Conception to Production

## Summary
Defines the 5-phase ADLC (Agent Development Lifecycle) for building production-ready Agentforce agents. Covers Agentforce DX (CLI tooling), agentSpec.yaml for declarative agent definitions, Python SDK for programmatic testing, STDM (Session Tracing Data Model) for observability, Agentforce Optimization and Moments for continuous improvement, and a table of common failure categories.

## Key Takeaways
- ADLC phases: Ideation → Development → Testing → Deployment → Monitoring/Tuning
- **Agentforce DX**: CLI for defining agents outside UI; enables version control and CI/CD
- **agentSpec.yaml**: Declarative agent spec — topics, actions, guardrails, prompt templates in code; deployable via SFDX
- **Python SDK**: Programmatic testing; enables assertions on agent outputs; CI/CD integration
- **STDM**: Logs every step, LLM call, action invocation, and decision — immutable audit trail; both for testing and production compliance
- **Agentforce Optimization**: Production tool for identifying topic misclassification, action failures, hallucination patterns
- **Agentforce Moments**: Specific interaction instances flagged for human review and iterative improvement
- **Common failure categories**: Topic misclassification, hallucination, action failure (governor limits/API timeout), guardrail false positives, escalation over-reliance

## Notable Quotes / Data Points
- Agentforce Moments as systematic improvement process — not ad-hoc review
- STDM enables both testing observability and production compliance audit trail in one framework
- Python SDK allows test suites with assertions — key for "agentic TDD"

## Wiki Pages Updated
- [[adlc]] — Full 5-phase framework, tooling, failure categories
- [[agentforce]] — DX tooling, STDM, Optimization/Moments capabilities

## Gaps / Follow-up
- agentSpec.yaml full schema not documented here — needs dedicated reference
- How STDM data retention policies work for compliance (GDPR, SOC 2) needs clarification
