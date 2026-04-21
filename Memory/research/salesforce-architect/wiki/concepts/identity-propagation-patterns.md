---
name: Identity Propagation Patterns
type: concept
category: governance
tags: [identity, security, obo, s2s, agents, mulesoft, flex-gateway]
sources: 1
last_updated: 2026-04-21
---

# Identity Propagation Patterns

## Definition
Mechanisms for carrying end-user identity (or service identity) through multi-hop agent call chains so that downstream APIs and data stores can enforce the correct authorization context. Without explicit identity propagation, agent-to-API calls default to a service account identity, which may over-privilege or under-privilege access.

## When to Use
- Whenever an AI agent makes API calls on behalf of a user (e.g., Agentforce agent calling a MuleSoft API that accesses user-specific CRM data)
- When cross-system authorization must reflect the originating user's permissions, not a generic service account
- In multi-vendor agent architectures where identity must cross organizational or platform boundaries

## How It Works

### MuleSoft Trusted Agent Identity Framework
MuleSoft Flex Gateway enforces identity propagation as an **outbound policy** on every agent-to-API call. Three patterns supported:

#### 1. On-Behalf-Of (OBO) — RFC 8693 Token Exchange
- **Use case**: Agent acts on behalf of a known, authenticated user; downstream API enforces user-level authorization
- **Mechanism**: 
  1. Agent holds a subject_token (user's JWT from Agentforce/IDP)
  2. Flex Gateway calls Authorization Server's token exchange endpoint
  3. AS validates subject_token, issues new access_token scoped to downstream API
  4. Agent calls downstream API with this delegated token
- **Trust model**: User's identity flows through; downstream sees user's permissions
- **When to use**: Public data access where user context matters; CRM data retrieval; personalized responses

#### 2. Server-to-Server (S2S) — Client Credentials
- **Use case**: Agent accesses non-user-specific data or performs system-level actions
- **Mechanism**: Agent authenticates with own client_id/secret; receives access_token for its own identity
- **Trust model**: Service identity; no user context propagated
- **When to use**: Reference data access, system metrics, configuration retrieval, bulk background operations

#### 3. In-Task Authorization Code — Cross-Domain Challenge
- **Use case**: Agent encounters a resource requiring authorization from a different domain/system during task execution
- **Mechanism**:
  1. Downstream API returns a 401 with a `WWW-Authenticate: Bearer realm="X"` challenge
  2. Agent Broker intercepts; escalates to human for authorization or triggers cross-domain OAuth flow
  3. Once authorized, agent proceeds with new token scoped to that domain
- **When to use**: Multi-cloud scenarios where agent crosses trust boundaries mid-task; external partner API calls requiring separate consent

### Enforcement Architecture
```
Agentforce Agent
    ↓ (carries user JWT)
MuleSoft Flex Gateway (outbound policy)
    ├── OBO: exchanges user JWT for downstream token
    ├── S2S: uses service credentials  
    └── In-Task AuthCode: challenges to domain IDP
              ↓
        Downstream API (enforces correct authorization)
```

### Identity Propagation in the 11-Layer Model
- Security layer: "Zero Trust Architecture with AI Verification" — just-in-time access for agents based on specific task
- Agentic layer: "Distributed Agent Policy Enforcement" — agents self-check compliance before taking actions
- The OBO/S2S/In-Task patterns are the implementation mechanisms for these architectural principles

## Key Constraints
- OBO tokens expire; agent sessions spanning long workflows need refresh logic
- S2S gives service-level access — over-privileging risk if service account has broad permissions
- In-Task Authorization Code requires human-in-the-loop for some cross-domain scenarios — adds latency
- Identity propagation only enforced at Flex Gateway; agent-to-agent (A2A) calls between Salesforce agents use Agentforce's own trust model

## Related Patterns / Alternatives
- [[mulesoft-agent-fabric]] — Flex Gateway as the enforcement point for all three patterns
- [[mcp-a2a-protocols]] — A2A calls also need identity propagation between agents
- [[data-360-security-architecture]] — ABAC/CEDAR enforces authorization at the data layer using attribute claims from propagated tokens

## Dennis's Take
OBO is the right default for most agentic use cases — it gives you user-level authorization at the downstream API and avoids over-privileging. Only use S2S for genuinely non-user-specific operations. The In-Task pattern is elegant but adds complexity — worth it for multi-cloud architectures where cross-domain consent is unavoidable.

## Sources
- [[end-user-identity-propagation-agents]] — Full spec of all three patterns, Flex Gateway enforcement, RFC 8693 details
