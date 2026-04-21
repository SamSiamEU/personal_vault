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
Practical implementation guide for the five Agentforce agent types with specific CRM use cases and architectural blueprints. Covers conversational agents (messaging + email SDR), proactive agents (external and internal event response), ambient agents (stream observer + activity interception), autonomous agents, and collaborative agents. Includes trade-off tables and related pattern cross-references for each recipe.

## Key Takeaways
- **Conversational — Interactive Messaging**: Multi-channel (WhatsApp, SMS, Slack, Experience Cloud); four components — Topics/Instructions, Actions, Guardrails, Prompt Templates; Data 360 vector store + RAG for knowledge grounding; Live Agent escalation with full conversation context injected
- **Conversational — Email SDR Agent**: Async multi-turn email; BANT qualification; schedules meetings via Task/Meeting Scheduling; 5-minute first response vs. 8-24h for humans; 2-5x SDR capacity increase
- **Proactive — External Event Response**: External system → Pub/Sub API or Data 360 streaming → subscriber Flow → Agent Action → notify/act; 24/7 event triage without human overhead
- **Proactive — Internal Salesforce Event Response**: CDC/Platform Events/RTEM → Flow/Apex → Agent Action; intelligent triage beyond simple rule-based routing
- **Ambient — Stream Observer**: Attaches to video/audio call stream; real-time objection handling, sentiment analysis, coaching; window size vs. accuracy trade-off
- **Ambient — Activity Interception**: Observes UI actions; surfaces knowledge articles and next-best-actions without user prompts; fraud/threat detection in real time
- **Collaborative**: Human-in-the-loop model — Conversational initiates, Proactive handles backend, Ambient provides guidance; multi-team cross-org workflow
- Trade-off tables for each pattern clearly show gain vs. cost (latency, accuracy, scalability, cost)

## Notable Quotes / Data Points
- Email SDR: "<5 min first response (vs. 8–24 hrs)" and "2-5x increase in lead coverage"
- Ambient stream observer: high-quality audio = better accuracy BUT more latency — tuning required per use case
- Collaborative pattern: "a seamless fusion of human and digital labor"

## Wiki Pages Updated
- [[agentforce]] — Five agent types, action/guardrail/prompt template architecture
- [[agentic-design-patterns]] — Implementation details for conversational/proactive/ambient/collaborative patterns
- [[data-360]] — Data 360 as grounding layer for all agent types

## Gaps / Follow-up
- Only read lines 1-400 of this file (~30k token file); autonomous agent pattern not fully covered — re-read offset 400+ for autonomous agent section
- Chapter 4 "Integration Patterns for Agents" referenced but not yet ingested from this file
