---
title: Agentforce Implementation Guide (Customer)
type: source
format: pdf
url: raw/agentforce_implementation_customer.pdf
author: Salesforce
date_published: 2025-10-17
date_ingested: 2026-04-21
tags: [agentforce, adlc, implementation, customer-guide]
---

# Agentforce Implementation Guide (Customer)

## Summary
Customer-facing guide to implementing Agentforce agents end-to-end. Uses fictional Makana Medical Devices as a worked example throughout. Covers the full 5-stage lifecycle: Ideate → Build → Test → Deploy → Monitor. More hands-on and prescriptive than the ADLC whitepaper — focuses on what a customer team actually does in each phase rather than abstract architectural principles.

## Key Takeaways

### Stage 1 — Ideate
- Use case definition: choose a use case with clear business value, measurable KPIs, and human oversight capability
- Risk management: assess data sensitivity, regulatory constraints, failure modes
- Guardrails design: define what the agent can and cannot do before writing a single topic
- Output: signed-off agent spec (maps to agentSpec.yaml in Agentforce DX)

### Stage 2 — Build
- Create agent in Agentforce Studio: configure agent type, topics, actions
- Einstein GenAI: configure LLM, grounding data, prompt templates
- Topic design: each topic = a bounded capability with defined triggers and actions
- Action types: Flow actions, Apex actions, external service calls, Einstein GenAI prompts
- Makana example: "Order Status" topic → triggers on order inquiry intent → calls Flow to query Order object → responds with structured status

### Stage 3 — Test
- Validate agent responses against expected outcomes per scenario
- Iteration loop: adjust instructions, rephrase topics, tune guardrails
- Use Agentforce DX test harness for automated scenario replay
- Key test categories: intent recognition accuracy, action invocation correctness, guardrail enforcement, edge case handling

### Stage 4 — Deploy
- Connections: configure channel (Messaging, Slack, Experience Cloud, etc.)
- Channel routing: define when to escalate to human agent (Omni-Channel routing rules)
- Messaging configuration: set up session handling, timeout behavior, handoff messages
- Permissions: assign agent to user profiles or permission sets

### Stage 5 — Monitor
- Agentforce Analytics: tracks conversation outcomes, topic resolution rates, escalation rates
- Optimization loop: identify low-resolution topics → refine instructions → re-test → redeploy
- Moments: surface agent-in-flight conversation snapshots for quality review
- KPI tracking: connect agent metrics to original business KPIs defined in Ideate stage

## Notable Quotes / Data Points
- Makana Medical Devices fictional example used throughout — good reference for explaining ADLC to customers
- Guardrails and topic scope design emphasized as most critical decisions in Ideate phase
- Monitor phase feeds directly back to Build phase — continuous improvement loop is explicit

## Wiki Pages Updated
- [[adlc]] — Customer-facing ADLC aligns with whitepaper phases; adds Build detail (topics/actions/Einstein GenAI setup) and Monitor detail (Agentforce Analytics, Moments, KPI loop)
- [[agentforce]] — Build stage details (topic/action types), Deploy stage (channel routing, Omni-Channel integration)

## Gaps / Follow-up
- Read first 200 lines (pdftotext); remainder not read — may contain deeper technical implementation details
- Makana example may contain concrete Flow/Apex patterns worth extracting as solution patterns
