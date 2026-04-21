**Enterprise Agentic Architecture and Design Patterns** brings structure to the possibilities of multi-agent architectures, identifying and highlighting how capabilities novel to AI agents may be combined to deliver reliable, repeatable, scalable, and manageable agentic solutions. Taking inspiration from “Design Patterns” for Object Oriented programming, we lay out patterns that can be combined and extended to solve the many exciting challenges that prior to agentic technologies lay outside the scope of business systems built on traditional deterministic technologies.

Following discussion of the rationale for multi-agent architectures we introduce numerous agentic patterns, from simple patterns that leverage natural language processing to determine user intent, to multi-agent patterns that provide for separation of concerns between agents, to UX agentic patterns that bring agentic reasoning to the presentation and interaction with systems, information, and content.

First and foremost you will get a new way of thinking about agents - agents as components, agents as composers, agents as actors, agents as collaborators, and most importantly agents within a larger architecture that act with intent and act within their individual scope of concerns.

You will get the pointers you need to conceive of rich agentic solutions that span user journeys and inform significant agentic experiences, experiences that have never been possible before.

The initial sections of this document provide the rationale for muti-agent architectures. Read these for a better understanding of the challenges and opportunities that multi-agent architectures present.

Following are definitions and descriptions of agentic patterns, from simple to complex, covering patterns that support interactions, patterns for specialist agents, patterns for background operations, and long-running patterns. Each pattern includes a diagram of the key components that realize the pattern, plus recommendations for usage and representative use cases.

Lastly, the appendix includes examples of how these patterns are combined into holistic agentic solutions supporting a larger agentic experience, for example, to support Customer Service or Brokered Sales. Reference this section to see how a rich agentic experience leverages decomposition and separation of concerns at the agent and action level to drive reuse at the interaction level, with shared agents supporting both internal and external constituents, in both assistive and autonomous modes.

As enterprise architects integrate Generative AI into their ecosystems, they must address a common set of design questions:

- How many agents are required?
- How will agents interoperate?
- What’s the division of labor between agents and humans?
- How are these components assembled into a coherent system?

This document presents a pattern-based methodology for designing and building agentic solutions.

*Monolithic* agents are the starting point for most agentic solutions. Agents—and more specifically, Agentforce agents—are capable performers across a range of topics. For common use cases, start with a single agent.

As your organization grows, multi-agent architectures are the preferred approach. *Multi-agent architecture* enables greater scale, control, and flexibility compared to monolithic, single-agent systems.

Multi-agent architecture provides these key benefits:

- **Increased Performance & Complexity Breakdown**: A system of multiple, specialized agents provides increased capabilities and simplifies instruction adherence.
- **Modularity & Extensibility** agents can be added, replaced, modified, and tested with greater ease, which promotes agility.
- **Resilience & Fault Tolerance**: The failure of a single component doesn’t compromise the entire system, which leads to better overall resilience.
- **Decentralized Governance**: Troubleshooting and management can be isolated to specific agents and their corresponding applications, which simplifies maintenance and oversight.
![Salesforce Agentforce Architecture](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Agentforce-Arch.png)

Rationalizing a multi-agent architecture starts with projecting core architectural principles onto the capabilities and structure of agents. The resulting multi-agent architectures are then a manifestation of core system design and system architecture principles that are aligned with the unique “grain” of AI technologies.

Key principles that drive this architecture include:

- Manage complexity through decomposition
- Improve resilience and reduce brittleness through decoupling
- Improve dependability and efficiency through code reuse
- Improve agent reliability by limiting any one agent’s scope of concerns
- Improve system maintenance and evolution through modularity and extensibility
- Simplify agent management and accountability though specialization

Unlike more primitive agentic architectures (for example, those that focus on LLMs as the core architectural construct), *Agentforce was designed for multi-agent orchestration from its inception*. Multi-agent orchestration underlies the Atlas Reasoning engine and agentic reasoning to create dynamic, effective programming paths within an agentic response to dramatically expand the ability to deliver a broad, deep agentic augmentation to the user experience (UX).

Within Agentforce this type of coordination is enabled by these key open, interoperable protocols and Salesforce Products:

- **Agentforce** provide an Agent sub-system to encapsulate all of the key elements of an agent: topics, instructions, actions, guardrails, context, invocations, outputs, execution details, logs, etc.
- **Actions**: provide hooks to access data, call flows, invoke external systems, and call other agents.
- **Data 360**: provides a data virtualization layer to bring specific, individualized context to the agent (leveraging Data 360’s unified profile and key chain to pull specific information from across the enterprise).

And for agents across the enterprise or to access agents or resources, we support:

- **Model Context Protocol (MCP)**: is a secure communication layer that connects agents to enterprise tools, data, and knowledge to ensure contextual accuracy.
- **Agent-to-Agent (A2A) Protocol**: is a standardized handshake for inter-agent delegation that enables secure, governed coordination across systems, orgs, and vendors.

These principles provide the foundation for building a scalable, governable system of orchestrated intelligence.

Robust agentic solutions require clear approaches to the non-functional requirements that underpin effective technology delivery:

- Security and Governance (Identity and Access Management, Data Privacy, Data Security, and Threat Modeling).
- Observability & Monitoring (Distributed tracing, Centralized Logging, Metrics, and Dashboards).
- Operationalization and Lifecycle Management (Specification, Test Case Generation, Testing, Feedback, Continual Learning, Deprecation).

These are key architectural considerations for building Enterprise Agentic solutions that aren’t covered in this whitepaper; however, they will be addressed in future publications.

To manage an enterprise-wide agentic landscape, architects must classify agents through two complementary lenses: technical function and business impact.

This taxonomy categorizes the functional roles that agents may assume within an architecture.

- **Channel/UX Roles**: Define the modality of interaction (for example, Headless, Prompt, Chats and Messages, or AI-Managed Workspaces).
- **Specialist Roles**: Encapsulate deep-domain knowledge (for example, Domain Expert, Knowledge Minion, Assistant, or Planner).
- **Utility Service Roles**: Perform discrete, transactional tasks (for example, Generation, Summarization, Transformation, or Configuration).
- **Maintenance & Proactive Service Roles**: Focus on data health and quality (for example, Curation, Conformation, Data Quality, or Data Enrichment).
- **Long-Running Roles**: Manage processes over extended periods of time (for example, Concierge, Project Manager, Nurturer, or Watcher/Alerter).

To facilitate clear design and communication, the **Agentic Map** is the standard template to describe agentic solutions. It defines key entities, systems, and interactions within a specific design pattern.

Here are the Agentic Map Template Components:

- **User Layers** define the human actors in the system (for example, Customers, Authenticated Employees (SF-Users), and Non-Authenticated Employees).
- **Agent Layers** describe required agents, exhibited patterns, relationships with one another, and instructions that are used to actualize specific patterns.
- **Context/Actions** are the resources, capabilities, or actions that the agent manages or accesses.
- **Sources** are the underlying data, applications, knowledge bases, and other systems that the agents connect to.

Appendices A and B illustrate system-level agentic patterns by demonstrating their composition within the Agentic Map Template swimlanes.

At Salesforce, we use a library of agent patterns to organize and deliver reliable, predictable agentic solutions. These patterns are our blueprints for solving common architectural problems.

They’re grouped into four primary categories:

- **Interaction Patterns**: Focus on agentic engagement and user experience (UX).
- **Specialist/Worker Patterns**: Encapsulate deep knowledge or specific skills within a particular domain.
- **Utility & Data Management Patterns**: Perform specific, often repeatable tasks that support other agents or processes.
- **Long-Running Patterns**: Manage processes and workflows that occur over extended periods, involving multiple steps.

The following sections detail key patterns from each category. Each pattern description provides an **Overview**, **Output Type**, **Pattern Use Guidance**, **Representative Use Cases**, and a **Solution Diagram**, as well as mapping to the **Salesforce Agentic Maturity Rubric**.

*Interaction patterns* are foundational designs that focus on agentic engagement and user experience.

- **Overview**: The *Greeter pattern* is a simple, easy-to-implement pattern that uses natural language to determine user intent. Then, it routes the user to the appropriate human agent.
- **Output Type**: Hand-off/Escalate to the next resource.
- **Business Value**: Facilitate a seamless, efficient first contact for customers while maximizing intent resolution and context collection for service providers.
- **Pattern Use Guidance**: Configure the agent as the primary engagement resource for brand channels. Provide instructions on brand, products, and services that are paired with routing instructions based on user intent. The agent collects and summarizes intent to deliver a warm handoff.
- **Representative Use Case**: Imagine a web page that uses a chat bot to present a menu of options where users must click through all of the options before they’re routed to a human. To improve back-office productivity and efficiency, chatbots often use complex, complicated work paths and interactions. This leads to a “fill, choose, and click” fatigue scenario for customers that often results in frustration if their context lies outside of the available menu options. By replacing traditional chatbots with the *Agentic Front Door* —which uses natural language interactions—it eases the burden and provides a human-like interaction.
- **Agentforce Recipe**:
	- Agentforce Service Agent: [Build a Service Agent](https://trailhead.salesforce.com/content/learn/projects/quick-start-build-your-first-agent-with-agentforce)
		- The packaged Service Agent has configurable transfer capabilities that support transfer:
			- To human agents
						- To AI agents
						- To external agents
		- Industry specific patterns that contain code examples
- **Diagram**: ![Greeter Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Greeter-Pattern.png)
- **Salesforce Agentic Maturity**: Level 1 (or Level 0 if you use the Out-of-the-Box Service Agent with built in transfer and escalation)
- **Overview**: The *Operator pattern* builds on the *Greeter pattern* by routing requests to the appropriate specialist agent or human and negotiating intent (if needed).
- **Output Type**: Hand-off/Transfer to the next resource.
- **Pattern Use Guidance**: Pair brand- and service-specific instructions with instructions on where to send the user based on intent. Define escalation resources, which may be humans or other agents.
- **Representative Use Case**: Use the *Agentic Front Door* for scenarios where there’s a high degree of specialization among human or AI representatives.
- **Diagram**: ![Operator Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Operator-Pattern.png)
- **Salesforce Agentic Maturity**: Level 2
- **Overview**: The *Orchestrator pattern* manages an AI Agent "Swarm." When it receives a user request, it passes the utterance to one or more specialist agents, and then aggregates the responses for the user. Unlike the *Operator pattern*, it remains the first point of contact (POC).
- **Output Type**: Collate and prepare response(s) from worker agents.
- **Pattern Use Guidance**: Configured as the primary engager. Provide instructions for each supporting worker agent (for example, a Prioritizer or Domain SME) that allows the orchestrator to relay utterances to them.
- **Representative Use Case**: Use the *Orchestrator Pattern* as the agentic front door to assist customers who may need to discuss multiple topics per conversation, which requires multi-agent solutions and consistent interactions. In a multi-system architecture, consider the *Orchestrator Pattern* to coordinate responses across systems and with the collaboration of external agents.
- **Diagram**: ![Orchestrator Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Orchestrator-Pattern.png)
- **Salesforce Agentic Maturity**: Level 3
- **Overview**: The *Listener/Feed pattern* surfaces context and insights during the flow of a conversation. The *Listener* is triggered during each conversational turn to find and display relevant information for an employee.
- **Output Type**: Provide relevant context based on conversation, which can be formatted for effect (for example, making comparisons or highlighting key points).
- **Pattern Use Guidance**: Attach the Listener to a turn-based channel (for example, chat, voice, or SMS). Define topics for each subject area. The agent consumes the transcript, identifies topics, and invokes actions to search for and post relevant content to a running feed for the employee.
- **Representative Use Case**: Use the *Universal Assistant* to assist Customer Service or Sales representatives.
- **Diagram**: ![Listener/Feed Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Listener-Feed.png)
- **Salesforce Agentic Maturity**: Level 3
- **Overview**: The *Workspace (Radar O’Reilly) pattern* manages a responsive single-pane-of-glass UX in the flow of a conversation. It processes each utterance to update portions of the UX with relevant content.
- **Output Type**: Provide relevant context that’s located in a portlet within a larger single-pane-of-glass view.
- **Pattern Use Guidance**: An *Orchestrator* agent passes utterances to a suite of *Topic* agents. Each Topic agent assesses the statement to determine whether a UX update is necessary. If so, it pushes dynamic updates to the corresponding LWC.
- **Representative Use Case**: This functions like an advanced agentic front door.
- **Diagram**: ![Workspace (Radar O'Reilly) Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Workspace-Radar-O-Reilly.png)
- **Salesforce Agentic Maturity**: Level 3

*Specialist patterns* encapsulate deep knowledge or skills in a particular domain, and they’re typically orchestrated by *Interaction patterns*.

- **Overview**: The *Answerbot pattern* is an effective pattern for self-service that uses GenAI to determine natural language for knowledge retrieval, not just keywords.
- **Output Type**: Summarized knowledge and references/citations to supporting materials.
- **Pattern Use Guidance**: Organize and ingest reliable source materials (for example, Knowledge Stores or FAQs) to configure the agent. Position the agent on corporate websites or within internal portals. Monitor questions to identify and address knowledge gaps.
- **Representative Use Case**: Facilitating natural language searches on a corporate website, interacting with an HR Benefits Bot, and providing self-service components for all constituents.
- **Diagram**: ![Answerbot Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Answerbot-Pattern.png)
- **Salesforce Agentic Maturity**: Level 1
- **Overview**: The *Domain SME pattern* is a foundational pattern that provides a natural language front end for a business domain (for example, Orders or Claims).
- **Output Type**: Provide relevant content, topics, data, and formatted information about the domain.
- **Pattern Use Guidance**: Use this pattern to encapsulate a subject or business domain. Configure the agent with the ability to perform appropriate CRUD operations. Make these agents available through [*Interaction patterns*](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#6-interaction-patterns) (for example, - Orchestrator or Listener).
- **Representative Use Case**: Gatekeeping a business data domain, providing an "Order Agent" or "Inventory Agent," and providing an agentic interface for a business domain.
- **Diagram**: ![Domain SME Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Domain-SME-Pattern.png)
- **Salesforce Agentic Maturity**: Level 2
- **Overview**: The *Interrogator pattern* is an SME agent that can be interrogated on a topic to assemble context from multiple sources to answer questions. The key agentic capability leveraged is the ability to pull context and connect concepts across a body of content, in the way a human would after reading and internalizing the content. This pattern mitigates the need for "swivel-chair integration."
- **Output Type**: Provide answers to questions.
- **Pattern Use Guidance**: It’s often configured as a console widget that’s wired to the user's current context so they can ask questions directly. It’s also used in conjunction with knowledge resources like FAQs, Policies, and Product catalogs. Pair the *Interrogator pattern* with standard prompts to scale common answers to common questions.
- **Representative Use Case**: Use as a contract assistant agent; Benefit inquiries assistant, or specialist worker agent in multi-agent patterns (for example, Listener or Workspace).
- **Diagram**: ![Interrogator Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Interrogator-Pattern.png)
- **Salesforce Agentic Maturity**: Level 2
- **Overview**: The *Prioritizer pattern* is used to order a set of tasks or work objects based on a defined objective. It leverages GenAI for qualitative analysis, unstructured data analysis, or integrative analysis across multiple data domains.
- **Output Type**: Provide generative insight.
- **Pattern Use Guidance**: Use natural language to describe the desired qualities for prioritization. Ground the agent using a set of selectable options. Combine with the Listener pattern to create a responsive "Next Best Action" in the flow of work.
- **Representative Use Case**: Use as a *Next Best Action* generator or a specialist worker agent in long-running or multi-agent patterns.
- **Diagram**: ![Prioritizer Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Prioritizer-Pattern.png)
- **Salesforce Agentic Maturity**: Level 2

*Utility patterns* perform specific, repeatable tasks that support other agents or processes.

- **Overview**: The *Generator pattern* is a basic pattern for creating new content (for example, case summaries or email drafts) from existing inputs and standards. It’s often implemented as a prompt and may be embedded within other agents.
- **Output Type**: Provide generated content that conforms to the requested format and intent.
- **Pattern Use Guidance**: The *Generator pattern* can be used within most other patterns or as a standalone. Context can be provided through the request, hydration during execution, or additional enrichment steps.
- **Representative Use Case**: Provide case summaries, email drafts, knowledge articles, or proposals/responses to QBRs.
- **Diagram**: ![Generator Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Generator-Pattern.png)
- **Salesforce Agentic Maturity**: Level 1
- **Overview**: The *Data Steward pattern* is an autonomous, background pattern that introduces an agentic step into data operations to ensure consistent data quality, conformance, and enrichment.
- **Output Type**: Provide updated record and data fields prior to saving.
- **Pattern Use Guidance**: Embed data quality at the point of data creation by adding data stewards that record trigger flows prior to saving data. Helps to ensure consistent application of categorization, summary, and state data.
- **Representative Use Case**: Ensuring consistent "Pizza-Tracker" style updates, enriching account data, and eliminating mismatched zip codes and addresses.
- **Diagram**: ![Data Steward Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Data-Steward-Pattern.png)
- **Salesforce Agentic Maturity**: Level 2
- **Overview**: The *Zen Data Gardener pattern* is a scheduled background pattern that’s used to groom and standardize data, leveraging low-cost reasoning to validate, enrich, and conform data across otherwise unconnected data domains.
- **Output Type**: Provide updated records and/or data management tasks.
- **Pattern Use Guidance**: Use the pattern to enable regular, periodic data review and validation. For slow-changing data, schedule the agent on a slow cadence (for example, monthly). Combine with the [Data Steward Pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#data-steward-pattern) to provide prospective and retrospective data quality operations.
- **Representative Use Case**: Ensuring alignment between sold benefits and the claims system, as well as periodic validation of broker licenses against national registries.
- **Diagram**: ![Zen Data Gardener Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Zen-Gardener-Pattern.png)
- **Salesforce Agentic Maturity**: Level 4
- **Overview**: The *Configurer pattern* generates configuration artifacts (for example, SQL/SOQL, JSON, and CSVs) from natural language requirements. It can also run in reverse to validate an existing configuration against requirements.
- **Output Type**: Provide updated records, data management tasks, or build issues/errors for corrections.
- **Pattern Use Guidance**: Ground the agent using specific standards, guidelines, or examples. Configure build requirements using sources like contracts or product specs. Connect the *Configurer pattern* to the target system to push the generated configuration.
- **Representative Use Case**: Generating product configuration records for health insurance products and validating contract/payment terms for health providers.
- **Diagram**: ![Configurer Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Configurer-Pattern.png)
- **Salesforce Agentic Maturity**: Level 4
- **Overview**: The *Judge & Jury pattern* is designed to minimize hallucinations by using an ensemble of "juror" agents and a "judge" agent that assesses the congruence of responses to ensure they’re materially consistent and grounded.
	- The *Ensemble Approach* is embedded within Agentforce and the Atlas Reasoning engine to address response veracity and relevancy. The *Judge and Jury pattern* builds on this capability when high levels of accuracy are essential.
		- The combination of *Data Grounding* (for example, “find your answer in these records/documents”) and *Prompt Engineering* (for example, “only return an answer if it’s found in these records” or “validate your answer against this external source”) are also effective ways to minimize hallucinations.
- **Output Type**: Provide generative insight.
- **Pattern Use Guidance**: Use when there’s a strong need for consistent and grounded generative outputs. A *Judge agent* compiles a grounded prompt and passes it to two or more *Juror agents*, and then the Judge assesses the responses. For best results, use different models (for example, one from OpenAI and another from Anthropic), for each Juror agent.
- **Representative Use Case**: Provide high-fidelity, factually-grounded responses to minimize hallucinations.
- **Diagram**: ![Judge & Jury Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Jury-Pattern.png)
- **Salesforce Agentic Maturity**: Level 2
- **Overview**: The *Model of Models pattern* leverages multiple expert agents to generate a broad swath of perspectives, and then it extracts the consensus. Unlike the [Judge & Jury pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#judge--jury-pattern), this pattern embraces multiple points of view to enhance richness.
	- This pattern may also be called the Panel of Experts pattern when there are expert models with different Points of View (POV) that it may be useful to tap.
		- Unlike the Judge and Jury pattern where the intent is to ensure that the agentic response converges on a commonly accessible “truth,” the *Model of Models pattern* extends the scope of the response by leveraging diversity in the agentic environment.
		- This pattern assumes that there are additional agents that have a distinct POV. For example, in a multi-org, multi-agent environment, or an environment with multiple vendor-supplied agents across tech stacks, the *Model of Models pattern* provides a structure for integrating multiple POVs.
		- When considering this pattern also consider other, often more lightweight approaches:
		- Instead of defining multiple expert agents, specify multiple prompts and have the system work as an ensemble of prompts.
				- Leverage “grounding” through actions that access contextually appropriate data.
- **Output Type**: Provide generative insight.
- **Pattern Use Guidance**: An *Aggregator* agent's role is to form and return a rich POV based on the key concepts that the Model agents returned. Model Agents determine a response based on their unique POV.
- **Representative Use Case**: Use in situations that may benefit from bringing together disparate viewpoints to add to the quality of the responses. For example, a multi-system agentic environment where privileged agents (for example, an *ERP agent*) may have a POV that’s valuable and otherwise inaccessible.
- **Diagram**: ![Model of Models Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Model-of-Models-Pattern.png)
- **Salesforce Agentic Maturity**: Level 2

*Long-Running Process patterns* manage processes that occur over extended periods and involve multiple steps and actors.

- **Overview**: The *Project Manager pattern* is a complex pattern that oversees a long-running project. It coordinates activities, tracks completion, notifies users, and represents project status to stakeholders.
- **Output Type**: There are multiple outputs (for example, cases, tasks, status updates, and notifications).
- **Pattern Use Guidance**: Use as an umbrella pattern to support regular, repeated, multi-step activities. The *Project Manager pattern* takes an input template/outline of a project—includingtasks, roles, and dependencies—then it instantiates cases and activities and assigns them to users.
- **Representative Use Case**: Use for account installation management and enterprise sales engagement.
- **Diagram**: ![Project Manager Pattern](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Project-Manager-Pattern.png)
- **Salesforce Agentic Maturity**: Level 4

While patterns describe agent roles, *orchestration archetypes* define the system-level blueprints for how a fleet of agents collaborate. These archetypes clarify the roles of *Agentforce* as the orchestration brain and *MuleSoft* as the universal connector and adapter.

**Archetype 1: SOMA (Single Org, Multiple Agents)**

- **Definition**: Multiple agents collaborate within one Salesforce org that uses shared governance and data.
- **Architectural Flow**: In Agentforce, a *Supervisor agent* acts as a single front door, routing requests to *Specialist agents* within the org. For external functionality, agents use the *Agentforce MCP Client* with MuleSoft acting as an MCP-wrapper for non-MCP-enabled APIs.
- **Key Considerations**: This pattern centralizes the orchestration logic in Salesforce (similar to CRM context and Data 360) to preserve unified governance, identity, permissions, and observability.

**Archetype 2: MOMA (Multi Org, Multiple Agents)**

- **Definition**: Agents collaborate across multiple Salesforce orgs, which requires secure coordination across data and permission boundaries.
- **Architectural Flow**: A *Supervisor agent* in one org delegates a task to an agent in another org via the standardized *agent-to-agent (A2A)* protocol. This handshake ensures org-level trust, user identity flow, and shared conversation context.
- **Key Considerations**: This pattern preserves org autonomy while enabling enterprise-wide workflows, which provides a foundation for coherent agentic operations in complex, multi-org estates.

**Archetype 3: Multi-Vendor A2A (Salesforce-led Orchestration)**

- **Definition**: A *Supervisor agent* in Salesforce coordinates work across a mix of Salesforce-native agents and agents from other vendors (for example, Google/Vertex or LangGraph) via the A2A protocol.
- **Architectural Flow**: The *Supervisor agent* processes the request and orchestrates a plan, invoking internal and external vendor agents via the A2A protocol. For external systems that aren’t A2A-capable, *MuleSoft* can expose a "lightweight agent facade" that wraps the existing tool and communicates with the A2A.
- **Key Considerations**: This archetype keeps the orchestration brain close to CRM and Data 360 by using A2A to produce clean, governable composition without a separate orchestration tier.

**Archetype 4: Multi-Vendor A2A (MuleSoft-led Orchestration)**

- **Definition**: Orchestration is initiated from a non-Salesforce entry point, which requires a neutral, external orchestrator to perform reasoning and routing.
- **Architectural Flow**: A *UI agent* in an external system forwards the request to an orchestration service (conceptualized as *MuleSoft Conductor*), which interprets intent and plans the task. The conductor then uses the A2A to route calls to vendor agents, including Agentforce agents for CRM or service actions.
- **Key Considerations**: This pattern is for non-Salesforce entry points where a neutral orchestrator is architecturally preferable. It keeps the UX in the domain system while centralizing reasoning, governance, policy, and observability in MuleSoft.

These individual patterns and orchestration archetypes are architectural building blocks that are designed to be composed into end-to-end solutions. The Agentic Solution Map is used to visualize how these components are wired together.

- A *Member Services Solution* for a healthcare provider is a standard implementation of the SOMA archetype. It uses an Answerbot for anonymous users, an *Orchestrator* for authenticated members, and multiple *Domain SME agents* (for example, Case, Claims, and Benefits) to handle specific requests.
- A *B2C Broker Portal* is a complex composition that uses a Portal *Orchestrator* agent to invoke a long-running *Project Manager agent* for an RFP process, which in turn, uses *Headless*, *Data Steward*, and *Interrogator agents* for back-office data operations.

An agentic design pattern methodology provides the architectural discipline required to build robust, scalable, and maintainable enterprise AI systems. By breaking down complexity and promoting modularity, these patterns enable architects to deliver reliable, predictable agentic solutions.

The choice of orchestration archetype is a strategic decision based on where users work, where context resides, and how the enterprise governs the interaction between humans, agents, and systems. By understanding the distinction between building agents and orchestrating them—and by leveraging open protocols like *MCP* and *A2A* —architects can move beyond creating isolated bots to engineering a cohesive, governed, and distributed enterprise-reasoning system. This approach provides a shared language and a set of reusable blueprints to build a sustainable agentic architecture.

This appendix provides concrete examples of how agentic patterns are composed into system-level solutions.

This diagram illustrates how five foundational patterns can be wired together to create a common customer service workflow. ![Basic Pattern Composition](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Starter-Patterns.png)

1. **Answerbot**: An anonymous user asks a question, which is handled by a knowledge-based agent.
2. **Operator**: An employee's question is triaged by an Operator, which fields the conversation and hands it off to a more specialized agent.
3. **Orchestrator**: An authenticated user (SF User) engages with an Orchestrator that coordinates multiple agents to handle a potentially multi-faceted inquiry.
4. **Domain SME**: Specialist agents (for example, HR Agents or Benefits Agents) are invoked by the orchestrator to perform subject matter updates and retrieve specific data.
5. **Generator**: Utility agents are used to summarize account details or wrap up a case after the interaction is complete.

This solution map details an agentic architecture for a Member Services use case, demonstrating the composition of multiple patterns.

- **User Profiles**: The solution serves three distinct user types: Anonymous User, Authenticated Member, and SF User (for example, a human CSR).
- **Interaction Patterns**: An *Answerbot* handles anonymous "Find-A-Doc" queries, while an Orchestrator (Agentic Front Door) manages authenticated user inquiries. A *Listener/Feed pattern* assists the SF User.
- **Domain Agent Reuse**: Specialized *Domain SME agents* (for example, Case Agent, Claims Agent, or Benefits Agent) are reused across different interaction flows.
- **Autonomous & Assistive**: The system combines *autonomous agents* (to direct user interaction) and *assistive agents* (to augment human CSRs).
- **Data Sources**: The architecture integrates a mix of public and enterprise data sources, with extensive use of *Data 360* and *MuleSoft* for connectivity.
![Member Services Example](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Member-Services-Example.png)

This diagram illustrates a logical architecture for an Assistive AI solution in a Contact Center, organized into functional layers.

- **Orchestrator Agents**: Manage user experiences for different personas (for example, Anonymous, External Member, or CSR) and orchestrate the overall interaction flow.
- **Worker Agents**: *Multiple SME agents* are focused on core business domains like Knowledge, Case/Claims/Benefits, and Provider Directory. A *Next Best Action* agent is also included.
- **Utility Agents**: Perform specific, reusable tasks such as Translation, Case Wrap-Up, and Call Summary. Integration & Core Systems: The entire agentic system is connected via a cross-platform integration layer to unstructured data resources, structured data resources, and core enterprise systems.
- **Governance**: A governance layer provides observability, evaluation, and management for the LLMs/SLMs that are used by the agents. ![ Contact Center System Architecture](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Contact-Center.png)

This solution map details a complex, long-running agentic interaction for a B2B health insurance broker portal. The model includes a *Portal agent* (*Orchestrator*) that facilitates the broker's journey through multiple steps (for example, submitting an RFP and receiving a proposal). This orchestrator invokes a *Project Manager* agent, which in turn, coordinates several headless agents for back-office data quality and transformations, such as an RFP Extractor, Census Transform, and Data Steward. ![Broker Portal Agentic Solution Map](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Broker-Portal-Example.png)

This diagram shows a logical architecture for a B2C Broker solution, which demonstrates a similar layered approach to the Contact Center. It includes *Orchestrator agents* for different user personas, reusable *Worker agents* for key domains (for example, Knowledge, Member Services, or Commissions), and *Utility agents* for specific functions like translation and summarization. ![B2C Broker Agent System Architecture](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Broker-Agents.png)

This diagram shows a logical architecture for a Provider Contracting solution. *Orchestrator* agents manage complete interactions, *Worker agents* manage specific intents within a domain (for example, a Contracting SME agent), and *Utility* agents perform discrete tasks like comparing contracts or generating insights. ![Provider Contracting System Architecture](https://a.sfdcstatic.com/developer-website/prod/images/architect/Ent-Agentic-Design-Patterns-Provider-Contracting.png)

The following table summarizes several key interaction patterns, typical user experiences, and primary architectural purposes.

| Pattern | User Experience (UX) | Purpose |
| --- | --- | --- |
| Greeter | Turn-by-turn text (Chat, Voice, SMS, and so on) that ends with the responder transferring the interaction to a human | This is a simple pattern that’s used to determine user intent, and then route the user to the appropriate human agent. |
| Operator | Turn-by-turn text (Chat, Voice, SMS, and so on) that ends with the responder transferring the interaction to a human or Specialist agent | This is used to route requests to appropriate hybrid agents. Building upon the Greeter, it’s a simple pattern that negotiates intent, and then transfers the interaction to a specialized human or AI agent. |
| Orchestrator | Turn-by-turn text (Chat, Voice, SMS, and so on) with the responder collecting and aggregating Specialist agent responses and delivering it to the UX | This is used to coordinate a managed AI-Agent “Swarm” that responds to a conversation as it progresses. An Orchestrator agent passes each turn's text through to one or more specialist agents, and then it aggregates the responses from each one. |
| Answerbot | Prompt and response | This is a natural language interface that uses knowledge resources, FAQs, policies, and so on to form responses. |
| Interrogator | Prompt and response | This is a natural language interface that’s used to ask questions in a specific domain or area. |
| Listener / Feed | Turn-by-turn text (Chat, Voice, SMS, and so on) that ends with the Orchestrator pattern feeding a Linear Feed | This is used to surface context and insights in the flow of conversation. |
| Workspace (Radar O'Reilly) | Turn-by-turn text (Chat, Voice, SMS, and so on) that ends with an adaptive, single-pane-of-glass heads-up-display | This is used to manage a responsive, single-pane-of-glass UX in the flow of conversation. |

David Harshbarger is a successful entrepreneur and technology leader who has worked for many leading software companies, architecting solutions that align the grain of architecture with the grain of the business so that technologists are working with, not against, their enabling technology. Today, David works as a Principal Enterprise Architect at Salesforce, supporting Health & Life Sciences.

Chacha Choudhury is a highly accomplished and visionary IT CTO/Chief Architect with decades of experience, currently serving as a Principal Enterprise Architect leading the Salesforce Architecture Program and Global Community of Architects. He is recognized for his expertise in setting enterprise-wide technology strategy, driving architecture modernization, and pioneering innovative solutions, including Generative AI and Agentic AI applications.