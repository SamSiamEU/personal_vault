As enterprises embrace the agentic paradigm, a new security challenge emerges: **How does end-user identity flow through a network of autonomous AI agents?** In traditional API architectures, a user authenticates once and the application calls backend services on the user’s behalf. The identity chain is short, well-understood, and typically managed within a single trust domain. Agentic architectures, however, feature much longer chains where a single request fans out across various agents, services, and Model Context Protocol (MCP) servers,each potentially crossing service boundaries, trust domains, and even organizational borders. Without a deliberate strategy for identity propagation, enterprises face a choice between security and functionality–a dilemma no architect should have to face.

MuleSoft addresses the complexities of identity propagation with its [**Trusted Agent Identity**](https://www.mulesoft.com/ai/trusted-agent-identity/announcement) feature. This solution utilizes a policy-based, gateway-managed strategy to ensure end-user identity is maintained across various interaction types—including agent-to-agent (A2A) protocols, MCP tool calls, and REST API requests.By centralizing identity management at the Flex Gateway layer through [outbound authentication policies](https://docs.mulesoft.com/gateway/latest/policies-outbound-directory), enterprises can secure their entire agent network without modifying backend services or agents.

This document walks through the identity propagation challenge using a progressive series of scenarios, each introducing additional complexity. Together, these scenarios illustrate why [Trusted Agent Identity](https://www.mulesoft.com/ai/trusted-agent-identity/announcement) is a foundational requirement for any enterprise-scale agent deployment.

In a conventional application, the identity flow (OAuth JWT flow) is straightforward: The user logs in, receives a token, and the application uses the token to access backend resources. The token is embedded with the user's identity–including who they are and what they’re authorized to do– and travels with every request. The call chain is short, typically one or two hops, and identity propagation is solved.

Agentic architectures, however, feature much longer call chains where a single user request might fan out across various agents, backend services, and Model Context Protocol (MCP) servers.Each request destination constitutes a separate hop. While these challenges–such as multi-hop identity propagation, mixed authorization models, cross-domain trust boundaries–are common in any distributed API setup, what *is* distinct is how the current ecosystem responds by default.. Today, the dominant pattern for agent-to-agent and agent-to-API communication relies on **client credentials**, **API keys**, or **shared secrets**. This means:

- **User identity is lost by default.** When an agent calls an MCP server or downstream API using client credentials, the request carries the agent’s service identity and not the end user’s. The downstream service has no way to know *which user* initiated the action, making per-user authorization and audit trails impossible.
- **Mixed authorization needs are ignored.** Not every downstream service requires user-context.While some manage user-specific information like transactions or portfolios, others provide public-facing or system-level data such as reference material or market trends.Because the current standard relies exclusively on client credentials, there is no way to differentiate between these needs or to selectively propagate user identity only when necessary.
- **Cross-domain trust boundaries are unaddressed.** Agents in B2B and regulated scenarios may need to interact with systems governed by entirely separate identity providers (IdPs). For example, an external banking system cannot interpret a corporate single-sign-on (SSO) token, yet it must still receive the user's consent and intent.. Client credentials flow has no mechanism for this.

The result is a gap between the enterprise requirement for user-attributable, least-privilege access and the current ecosystem's reliance on service-level authentication lacking user context. Closing this gap requires a deliberate, layered approach to identity propagation. To illustrate these concepts, the following scenarios utilize **Finport**, a fictional fintech application, to provide practical examples of these architectural patterns.

Finport is a fictional consumer-facing Fintech portfolio management web application backed by an agentic architecture. An Agent Broker (built using [MuleSoft Agent Broker](https://www.mulesoft.com/ai/agent-broker)) coordinates multiple downstream agents and MCP servers to fulfill user requests.

Finport exposes three core functionalities, each with a distinct identity requirement:

1. **"Show me my portfolio.":** The user requests their personal holdings and transaction history. Because this data is user-specific, the downstream Portfolio Service Agent and Portfolio MCP Server must know *which* user's data to return and must verify the user is authorized to access it. User identity must be propagated through every hop.
2. **"What are the current market trends?"**: The user requests public market data and asset prices. Because the data is public and doesn’t vary by user, the downstream Market Data Agent and Asset Market MCP Server don’t need, or expect, a user-scoped token. The broker's own service credentials are sufficient.
3. **"Transfer $5,000 to my external savings account."**: The user initiates a fund transfer to a bank that uses a different IdP(for example, Auth0 instead of Okta). The user's Finport token is meaningless to the bank's system. The user must authenticate directly with the bank (inline within the conversation) before the transfer can proceed.

Each of these functionalities map to a different identity propagation pattern. The following scenarios build progressively from a standard baseline (without agents) through each distinct pattern, illustrating how outbound policies in Flex Gateway address each requirement without modifying the agents or backend services.

Before introducing agents, it’s essential to establish the baseline: a user authenticating with a client application and accessing a backend service.

![](https://architect.salesforce.com/ns-assets/user-identity-propogation/auth-context-propagation-0.png)

**The flow**:

1. The user opens Finport and is redirected to the IdP’s login page (for example, Okta).
2. The user authenticates (username, password, SSO, multi-factor authentication (MFA), and any other requirements).
3. The IdP issues a signed JWT access token to the Finport application.
4. Finport now has a user token that represents the user's identity: who they are, what scopes they have been granted, and when the token expires. It can present it to any downstream service on behalf of this user.

**What this establishes**: This process follows the standard OAuth 2.0 architecture pattern. The initial user token, validated by a trusted IdP, serves as the essential foundation for all subsequent operations. Every subsequent scenario builds on this token.

**The ask**: Once authenticated, the user initiates actions such as fund transfers, market analysis, or portfolio reviews. These requests are processed through an Agent Broker and may involve multiple downstream agents or MCP servers. *This raises critical questions: How is the user's identity maintained across these distributed requests? What happens when a downstream service uses a completely different IdP?*

The user asks the Finport agent to *"Show me my portfolio."* This interaction triggers a backend chain starting with the **Finport Agent Broker**, built using [MuleSoft Agent Broker](https://www.mulesoft.com/ai/agent-broker). The broker hands off the task to a **Portfolio Service Agent**, which in turn queries a **Portfolio MCP Server**. The user's initial authentication token must now travel through multiple hops to access the requested portfolio records.

![](https://architect.salesforce.com/ns-assets/user-identity-propogation/auth-context-propagation-1.png)

Passing the original token violates the principle of least privilege, while using a service account loses the user's identity.

The Finport Agent receives the user's token, but it cannot simply forward that same token to the Portfolio Service Agent, as it would violate the principle of least privilege and wouldn’t properly scope the request for the downstream service. Conversely, using a service account results in a total **loss of user identity**. The Portfolio Service Agent and the Portfolio MCP Server would have no way to know *which* user's portfolio to return, and the audit trail would attribute every action to the broker's service identity rather than the end user.

Flex Gateway resolves these identity propagation complexities transparently through its [**Outbound OAuth 2.0 Token Exchange policy**](https://docs.mulesoft.com/gateway/latest/policies-outbound-oauth-obo). This solution intercepts outbound requests at every hop in the call chain, exchanging the incoming user token with the IdP for a new credential scoped specifically for the downstream service. The policy supports both OAuth 2.0 Token Exchange ([RFC 8693](https://datatracker.ietf.org/doc/html/rfc8693)) and [Microsoft Entra ID On-Behalf-Of](https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-on-behalf-of-flow) protocols.

**Key architectural benefit**: This entire process is handled by [Flex Gateway outbound policy](https://docs.mulesoft.com/gateway/latest/policies-outbound-oauth-obo). The broker and agents contain *zero* authentication logic. Instead, they focus purely on business logic while the gateway layer enforces identity propagation.

**The flow**:

1. The user authenticates with Okta and the Finport application sends a request through Flex Gateway.
2. The broker receives the validated user token and determines the Portfolio Service Agent is needed.
3. Flex Gateway's outbound OBO policy exchanges the user token with the IdP for a token scoped to the Portfolio Service Agent.
4. The Portfolio Service Agent receives a properly scoped token and calls the Portfolio MCP Server.
5. Flex Gateway again exchanges the token, this time scoped for the MCP Server.
6. The Portfolio MCP server returns the user's specific portfolio data.
7. A complete audit trail exists. Every hop is attributable to the original end user.

**Why this matters**: Without OBO token exchange, enterprises must choose between forwarding the original token, which violates least privilege, or using service accounts, which risks losing user identity. The OBO pattern eliminates this tradeoff since the user's identity is preserved at every hop, each token is scoped to its target, and the agents themselves remain completely unaware of the identity mechanics.

Not every downstream service requires user context. The user asks the Finport agent, *"What are the current market trends?"* Unlike the portfolio request in Scenario 1, market trend data is public when it does not vary by user. The downstream **Market Data Agent** and **Asset Market MCP Server** do not need, or expect, a user-scoped token.

![](https://architect.salesforce.com/ns-assets/user-identity-propogation/auth-context-propagation-2.png)

**Propagating user tokens where they are not needed expands the attack surface.**

If the Finport Agent Broker were to propagate the user's token to the Market Data Agent using the [OBO pattern](#scenario-1-on-behalf-of-obo-propagating-user-identity-through-agents) from Scenario 1, it would work but would be unnecessary. Propagating user tokens where they are not needed expands the attack surface, creates unnecessary dependencies on the IdP for token exchanges, and violates the principle of least privilege. The Market Data Agent simply needs to know that the request comes from an authorized service, not which *user* is asking.

Flex Gateway’s [Outbound OAuth 2.0 Client Credentials policy](https://docs.mulesoft.com/gateway/latest/policies-outbound-oauth) handles this transparently. Instead of exchanging the user's token, the policy injects the broker's own service credentials via a client credentials grant into the outgoing request. The downstream Market Data Agent receives a properly authenticated service-level token where no user identity is propagated because none is needed.

**Key architectural benefit**: The identity propagation strategy is not one-size-fits-all, rather it’s determined per downstream route based on the nature of the data and the requirements of the target service. Flex Gateway's outbound policies make this configurable per route. The same Finport Agent Broker can participate in both OBO flows (in Scenario 1) and S2S flows without any code changes. The policy configuration on the egress gateway determines which pattern applies to which downstream call.

**The flow:**

1. The user asks the Finport agent,*"What are the current market trends?"*
2. The broker determines that the Market Data Agent is needed to fulfill the request.
3. Flex Gateway's outbound Client Credentials policy obtains a service-level token using the broker's own credentials (no user token is exchanged or propagated).
4. The Market Data Agent receives a properly authenticated service request and calls the Asset Market MCP Server.
5. The Asset Market MCP Server returns the public market data.
6. No user identity is present in the chain by design because none is needed for this type of data.

**Why this matters**: Flex Gateway's policy-driven framework empowers architects to select the optimal identity model for every interaction, resolving the difficult choice between universal user token propagation—which increases overhead and security risks—and global service account usage, which sacrifices user context and compliance.

The most complex identity scenario arises when an agent needs to interact with a system governed by a completely different IdP, one that does not recognize the existing user token.

**The scenario**: The Finport user asks the Finport Agent to *"Transfer $5,000 to my external savings account."* This request involves two distinct downstream paths:

1. The **Portfolio Service Agent** (OBO) path to verify the user's holdings
2. The **Transaction Agent → Transaction MCP Server → User's Bank** path to execute the actual transfer
![](https://architect.salesforce.com/ns-assets/user-identity-propogation/auth-context-propagation-3.png)

The Transaction Agent needs to interact with the user's bank, which uses its own IdP. The user's Okta token from Finport is meaningless to the bank's system, as the bank has no trust relationship with Finport's IdP. Neither the [OBO pattern](#scenario-1-on-behalf-of-obo-propagating-user-identity-through-agents) (from Scenario 1) nor the [S2S pattern](#scenario-2---server-to-server-s2s-when-user-identity-is-not-needed) (from Scenario 2) can solve this. OBO exchanges tokens within the same IdP, and S2S uses service credentials that carry no user identity at all. The bank requires the user to authenticate directly with their own banking credentials, potentially including MFA.

The [Outbound A2A In-Task Authorization Code policy](https://docs.mulesoft.com/gateway/latest/policies-outbound-a2a-intask-authorization-code) on Flex Gateway uses a challenge-response mechanism within the agent conversation. If a secondary token is missing when contacting the bank, the policy returns an auth-required challenge. This challenge includes all necessary details—such as endpoints, scopes, and PKCE parameters—for the client to initiate an OAuth 2.0 flow with the bank’s provider.

The Finport app then displays the bank's login inline for direct user authentication. Once completed, the client returns the token in the A2A request. The policy extracts this token for the bank's system and scrubs it from the message body to ensure security.

**Key architectural benefit**: The gateway policy layer orchestrates the entire cross-domain authentication process, ensuring that neither the broker nor the agents ever interact with raw credentials or require knowledge of the bank's IdP. By using this challenge-response framework, users maintain full control: they provide explicit consent to authenticate with external systems, while the resulting token is transmitted securely via the policy layer.

**The flow**:

1. The user asks Finport to initiate a transfer. The request flows through the broker.
2. The broker fans out, using the Portfolio (OBO) to verify holdings, and the Transaction (In-Task) to execute the transfer.
3. The Transaction path triggers an auth-required challenge from the In-Task policy on Flex Gateway.
4. The challenge propagates back to the Finport application, which presents the bank's login flow to the user inline.
5. The user authenticates with their bank, including MFA if required.
6. The bank token is included in the subsequent A2A request. The policy extracts it, sets it in the Authorization header, and forwards the request.
7. The Transaction MCP Server receives the request with the bank's token and executes the transfer.

**Why this matters:** Cross-domain identity is a major challenge in agentic architectures. Without in-task authentication, enterprises must either pre-establish complex trust relationships between every IdPin the network, or ask users to provide banking credentials to an agent. The In-Task pattern solves this by allowing direct user authentication with external providers; the policy manages token mechanics while keeping agents decoupled from external identity domains.

Across all three scenarios, a single architectural principle holds: **Identity propagation is enforced at the gateway layer, not within agents or services**. The agents and MCP servers contain zero authentication logic. Their role is restricted to processing authenticated requests and returning results, while the Flex Gateway outbound policy layer manages all identity-related operations.

![](https://architect.salesforce.com/ns-assets/user-identity-propogation/auth-context-propagation-finport-broker.png)

This works because Flex Gateway's [outbound authentication policies](https://docs.mulesoft.com/gateway/latest/policies-outbound-directory) intercept traffic at the right point: after the agent makes its routing decision, but before the request reaches the downstream service. The policy transforms the token–whether it’s an [OBO exchange](https://docs.mulesoft.com/gateway/latest/policies-outbound-oauth-obo), [client credentials injection](https://docs.mulesoft.com/gateway/latest/policies-outbound-oauth), or [in-task challenge-response](https://docs.mulesoft.com/gateway/latest/policies-outbound-a2a-intask-authorization-code) –and forwards a properly authenticated request. The downstream service never knows the difference, therefore the agent never has to care. Authentication logic is centralized at the gateway, not scattered across services. The backend services require no code changes and the same policy configuration can be reused across multiple routes.

This approach is also protocol agnostic. Because the policies operate at the HTTP layer, they apply consistently whether the agent communicates via REST, MCP, A2A, or webhooks. As documented in the [Agent Fabric Deep Dive](https://architect.salesforce.com/docs/architect/fundamentals/guide/mulesoft-agent-fabric-deep-dive), all A2A and MCP traffic is routed through Flex Gateway to ensure that policies are applied on every endpoint, which means identity propagation is enforced uniformly regardless of the communication protocol.

Three composable patterns cover the full spectrum of identity requirements in an agentic architecture:

| Pattern | Policy | User identity | User Interaction | Use Case |
| --- | --- | --- | --- | --- |
| **On-Behalf-Of (OBO)** | [OAuth 2.0 OBO Credential Injection Policy](https://docs.mulesoft.com/gateway/latest/policies-outbound-oauth-obo) | Preserved | None (transparent) | User-specific data within the same trust domain |
| **Server-to-Server (S2S)** | [Outbound OAuth 2.0 Client Credentials](https://docs.mulesoft.com/gateway/latest/policies-outbound-directory) | Not propagated | None | Public data, system-level operations |
| **In-Task Authorization Code** | [Outbound A2A In-Task Authorization Code](https://docs.mulesoft.com/gateway/latest/policies-outbound-a2a-intask-authorization-code) | Primary + Secondary | Required (inline authentication | Cross-domain, multi-identity-provider, high-risk operations |

These patterns are not mutually exclusive. As the Finport scenarios show, a single Agent Broker can use OBO for one downstream call, S2S for another, and In-Task for a third. The policy configuration on each outbound route determines which pattern applies. There are no agent code changes and no service modification, only policy.

The gateway-enforced patterns described above secure individual interactions, but identity propagation isn’t an isolated concern. It’s a foundational layer of the broader MuleSoft Agent Fabric governance model. As described in the [Agent Fabric Deep Dive](https://architect.salesforce.com/docs/architect/fundamentals/guide/mulesoft-agent-fabric-deep-dive), Agent Fabric is built on four pillars: [**Discover, Orchestrate, Govern, and Observe**](https://architect.salesforce.com/docs/architect/fundamentals/guide/mulesoft-agent-fabric-deep-dive#agent-fabric-four-pillars-together), and each one depends on a reliable identity chain to function effectively.

- **Discover**: The [Agent Registry](https://docs.mulesoft.com/general/learning-map-agent-fabric) catalogs agents and their capabilities. Agent metadata including authentication requirements enables brokers to understand which identity patterns each agent expects.
- **Orchestrate**: The Agent Broker coordinates multi-agent workflows. Flex Gateway transparently handles identity transformation at each hop, so the broker can focus on task decomposition and routing.
- **Govern**: All A2A and MCP traffic is routed through Flex Gateway, even if the target system is unsecured, to ensure that policies are applied on every endpoint. Outbound authentication policies are part of the governance layer.
- **Observe**: Agent Visualizer provides real-time observability through a dynamic, interactive map of agent interactions. With user identity preserved at every hop, traces and logs provide user-attributable audit trails across the agent network.

Without trusted identity propagation, governance is incomplete. You can catalog and orchestrate agents, but you cannot ensure they act within the boundaries of the user's authorization. Trusted Agent Identity closes this gap, ensuring that security and user context remain central to agentic workflows.

To implement these patterns:

1. **Understand the Outbound Policy Directory**. Review the complete set of [outbound authentication policies](https://docs.mulesoft.com/gateway/latest/policies-outbound-directory) available for Flex Gateway.
2. **Start with OBO**. The [OAuth 2.0 Token Exchange policy](https://docs.mulesoft.com/gateway/latest/policies-outbound-oauth-obo) addresses the most common identity propagation need: preserving user context across agent hops.
3. **Add In-Task for Cross-Domain Scenarios**: When your agent network crosses trust boundaries, the [A2A In-Task Authorization Code policy](https://docs.mulesoft.com/gateway/latest/policies-outbound-a2a-intask-authorization-code) provides the challenge-response mechanism for obtaining secondary credentials from the user.
4. **Leverage Agent Fabric**. Define your agent network in the [agent-network YAML](https://docs.mulesoft.com/anypoint-code-builder/af-project-files) with policy configurations that specify the identity model per route. The platform handles the rest.
- [MuleSoft Trusted Agent Identity Announcement](https://www.mulesoft.com/ai/trusted-agent-identity/announcement)
- [Delegated Access Control in MuleSoft Agent Fabric](https://blogs.mulesoft.com/news/delegated-access-control-mulesoft-agent-fabric/)
- [Outbound Authentication Policies Directory](https://docs.mulesoft.com/gateway/latest/policies-outbound-directory)
- [Outbound OAuth 2.0 Token Exchange (OBO) Policy](https://docs.mulesoft.com/gateway/latest/policies-outbound-oauth-obo)
- [Outbound A2A In-Task Authorization Code Policy](https://docs.mulesoft.com/gateway/latest/policies-outbound-a2a-intask-authorization-code)
- [Architecting the Agentic Enterprise with MuleSoft](https://architect.salesforce.com/fundamentals/mulesoft-architecting-agentic-enterprise)
- [MuleSoft Agent Fabric Deep Dive](https://architect.salesforce.com/fundamentals/mulesoft-agent-fabric-deep-dive)
- [MuleSoft Agent Fabric Documentation](https://docs.mulesoft.com/agent-fabric/)
- [RFC 8693 — OAuth 2.0 Token Exchange](https://datatracker.ietf.org/doc/html/rfc8693)

*For detailed implementation guidance, refer to the [companion implementation guide](https://blogs.mulesoft.com/dev-guides/identity-propogation-mulesoft-agent-fabric/).*

Nikhil Aggarwal is a Distinguished Engineer at Salesforce, where he leads architecture for MuleSoft and Salesforce Automation Clouds. Nikhil brings over 18 years of experience delivering large-scale products and is passionate about scalable architecture, intuitive developer experiences, and building high-performing teams. Prior to Salesforce, he led multiple initiatives in Microsoft Power Platform, Dataverse and Office 365 from concept to launch. His work continues to shape how modern enterprises connect systems, automate workflows, and unlock business value in the AI-first era.

Akash Trivedi is a Director of Engineering at Salesforce with over 18 years of experience building scalable, secure, high-performance enterprise systems. He works at the intersection of AI, enterprise architecture, and process intelligence, with a focus on cloud-native platforms and reliable solutions that operate at scale. Prior to Salesforce, he held engineering roles at Microsoft, where he contributed to products including Copilot, Dataverse, and Power Platform.