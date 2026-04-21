The paradigm of software is shifting from direct manipulation to goal-oriented delegation. At the forefront of this transformation are AI agents—autonomous, intelligent entities capable of understanding, reasoning, and acting on behalf of users. This whitepaper provides a technical exploration of the primary types of AI agents: Conversational, Proactive, Ambient, Autonomous, and Collaborative. It defines each type, presents specific Customer Relationship Management (CRM) use cases, and provides an architectural blueprint for building these agents on the Salesforce *Agentforce* Platform, complete with technical examples leveraging Flow, Apex, Data 360, Agent2Agent (A2A) communication, and Model Context Protocol (MCP) interoperability.

An AI agent is a system that perceives its environment and takes actions to achieve specific goals. While the concept is not new, the advent of powerful Large Language Models (LLMs) has supercharged their capabilities. We can categorize agents based on their primary mode of operation and interaction.

**Definition:** Conversational agents are the most familiar type of agent. They operate in a reactive, request–response manner, primarily through natural language interfaces (text or voice). Their core function is to understand user intent and provide a relevant response, whether it's answering a question, fetching information, or executing a simple command.

**Importance:** Conversational agents are the digital front doors to an organization. They excel at handling well-defined, repetitive tasks, thus freeing up human resources. Their effectiveness is measured by their ability to resolve user intent quickly and accurately, and to take actions on behalf of users.

![Conversational agents diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/conversational-agents.png)

**Definition:** Unlike conversational agents that wait for a prompt, proactive agents act as vigilant observers. They are triggered by specific events, data changes, or predefined conditions within a system. When triggered, they execute a task or initiate a workflow without requiring direct user interaction.

**Importance:** Proactive agents transform a system from a passive repository of data into an active participant in business processes. They identify opportunities and risks as they emerge, enabling businesses to act on critical signals in real time.

![Proactive agents diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/proactive-agents.png)

**Definition:** Ambient agents are a specific type of proactive agents that operate continuously in the background of a user's workflow without requiring explicit commands. Users often benefit from their actions without being consciously aware of their operation, because they are designed to augment human capabilities while maintaining a low profile.

**Importance:** The goal of an ambient agent is to reduce the cognitive load on users by automating the mundane "work about work." They make processes more efficient by seamlessly integrating into the tools employees use every day, capturing and structuring information automatically.

![Ambient agents diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/ambient-agents.png)

**Definition:** Autonomous agents represent a significant leap in complexity. They are given a high-level goal and are capable of independently planning and executing a sequence of steps to achieve that goal. They can reason, make decisions, and even learn from their actions to improve performance over time.

**Importance:** This is the closest we get to a true digital employee. Autonomous agents can be delegated a complex, multi-step objective, such as "Generate 50 new qualified leads in the manufacturing sector this quarter," and be trusted to formulate and execute a plan to achieve it.

![Autonomous agents diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/autonomous-agents.png)

**Definition:** Collaborative agents, often called "agent swarms," are a collection of specialized agents that work together to solve a problem that is too complex for any single agent to handle. An "orchestrator" or "master" agent often decomposes a large task, delegates subtasks to the appropriate specialized agents, and then synthesizes their outputs. A robust Agent2Agent (A2A) communication protocol achieves this.

**Importance:** This approach mirrors a human team. By breaking down a complex problem, each specialized agent can bring its unique skills to bear: one specializes in data analysis, another in customer communication, and a third in system integration, leading to a more robust and comprehensive solution.

![Collaborative agents diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/collaborative-agents.png)

Having explored the taxonomy of AI agents, a crucial question remains: how do we combine these elements to solve real-world business problems efficiently and reliably? This chapter answers that question by providing a repository of common agentic design patterns. Each pattern is a proven solution to a recurring challenge, offering a blueprint for everything from simple, single-purpose agents to complex, collaborative agent swarms.

Conversational agents are often the front door to an organization's AI capabilities. They are defined by their ability to engage in a stateful, multi-turn dialog, acting as the primary interface through which users perform tasks and retrieve information using natural language. This section presents two essential recipes for building conversational agents, each tailored to a specific channel: one for the rapid, interactive exchanges of messaging clients, and another for the structured, asynchronous nature of email.

A conversational agent's intelligence is derived from its ability to access and reason over the right data at the right time. This pattern relies on a sophisticated data foundation that connects to customer records, knowledge articles, and business analytics. The complete, reusable recipes for these integrations are available in [Chapter 4: Integration Patterns](#chapter-4-integration-patterns-for-agents).

**Problem**

Customers engage across many digital channels and expect **instant, contextual, and intelligent responses.** Traditional chatbots are either **scripted** or **data-blind,** which leads to poor personalization, early escalations to humans, and high service costs.

**Context**

- Your organization has multi-channel digital engagement (WhatsApp, SMS, Slack, and Salesforce Experience Cloud).
- Your organization's customers interact with your organization in [multiple languages](https://help.salesforce.com/s/articleView?id=ai.service_agent_considerations.htm&type=5).
- Your organization needs to augment service and sales workflows with agents that:
	- Pull from real-time, trusted customer data
		- Respect guardrails and compliance requirements
		- Escalate to human agents only when necessary
![Interactive messaging client pattern diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/interactive-messaging-client-pattern.png)

**Key Components**

- **Channel abstraction:** The Service Cloud Enhanced Chat (formerly Messaging for In-App and Web) allows the agent to communicate across multiple channels through a single experience.
- **Agentforce Service Agent:** The agent's behavior and purpose are defined by the following components.
	- **Topics and instructions:** Defines the agent's persona and conversational purpose for direct user interaction. This includes its core mission (for example, "You are an expert at solving customer support issues"), instructions on maintaining an empathetic and professional tone, and clear guardrails on the scope of inquiries it's authorized to handle.
		- **Actions:** Service-oriented actions that are tools the agent uses to diagnose and resolve customer issues in real time. These tools are designed to execute tasks like checking an order's status, searching a knowledge base for solutions, or creating a new support case directly from the conversational interface.
		- **Guardrails:** Guardrails act as a set of configurable rules and runtime checks that constrain the agent's behavior. Acts as a safety layer that can intercept prompts, validate the agent's proposed actions, and filter its final response to prevent harmful content, enforce business rules, and ensure the agent operates within its designated scope.
		- **Prompt Templates:** Reusable templates that are dynamically populated with live CRM data via merge fields or semantic data from Data 360 RAG Retrievers. These templates allow agents to generate contextual, on-brand content while the Einstein Trust Layer securely masks sensitive information before the instructions are sent to the LLM.
- **Data 360**
	- Data 360 components, including DLOs, DMOs, vector store, and RAG retrievers, provide the agent with a unified view of all relevant enterprise data, from structured customer records to unstructured knowledge articles, ensuring responses are accurate and contextually grounded.
- **Service Cloud**
	- **CRM data:** Connects the agent to the complete case history, providing crucial context on account details, contact records, and entitlements
		- **Live Agent queue:** Support for escalation and routing to a human service rep with the full conversation context injected

**Interactions**

1. Your organization's customer initiates conversation via a channel.
2. The message routes to **Agentforce,** which determines scope (topics) and applies guardrails.
3. AI composes responses using **prompt templates,** while Flow or Apex may trigger backend logic.
4. Context is retrieved from **Data 360 objects, vector store, and CRM** via RAG retriever.
5. AI returns a contextual answer.
6. If AI cannot resolve, the conversation escalates to the **Service Cloud Live Agent.**

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Response Speed | Always-on instant replies | 2+ seconds latency for complex queries |
| Accuracy | Grounded in real data via RAG | Requires curated, up-to-date vector store |
| Scalability | Near-infinite concurrent conversations | Costs must be optimized through caching, qualifying, and filtering |
| Flexibility | Handles open-ended queries | Requires sophisticated prompt engineering |
| Human Touch | Human service reps handle only complex cases | Customer frustration if escalation thresholds are wrong |
| Conversation Diversity | Large number of intents that requires different knowledge, skills, and tools | Requires continuous topic and instructions tuning to optimize accuracy and latency |

**Related Patterns**

[Greeter pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#greeter-pattern): A simple and easy to implement pattern that uses natural language to understand user intent and then routes the user to the appropriate service rep

[Operator pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#operator-pattern): Builds on the Greeter to route requests to the appropriate specialist AI agent or human service rep, negotiating intent if needed

[Orchestrator pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#orchestrator-pattern): Manages an AI agent swarm. It receives a user request, determines intent, creates a plan, passes the necessary data to one or more specialist agents, and then aggregates the responses for the user. Unlike the Operator, it remains the first point of contact.

**Problem**

Your customers largely use email-based asynchronous conversations, and this is still the best way for outreach. Your organization needs to reach these customers via email, but your sales development representatives can't reply to inbound emails within the SLA, leading to lead loss. Additionally, your workforce spends time on unqualified leads.

**Context**

- Your organization has email as a primary lead engagement channel.
- Your SDR has limited capacity to qualify leads at scale.
- Your sales process has multi-touch lead nurturing before they meet with SDRs or business development representatives (BDRs).
- Your organization needs to augment service and sales with agents that:
	- Pull from real-time sales enablement and sales product and marketing data
		- Respect guardrails and compliance
		- Schedule meetings based on lead qualification criteria
![Interactive email conversational pattern diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/Interactive-email-conversational-pattern.png)

**Key Components**

- **Email channel:** Handles capturing inbound messages, parsing their content and attachments, and maintaining thread continuity to enable asynchronous conversations.
- **Agentforce SDR Agent:** The agent's behavior and purpose are defined by the following components.
	- **Topics and instructions:** Defines the agent's mission to engage and qualify inbound leads through conversation. This includes instructions for understanding prospect needs, gathering key qualification data (for example, budget, authority, and timeline), and guiding the conversation toward a clear next step, such as scheduling a meeting with an account executive.
		- **Actions:** Specialized sales actions that enable the agent to manage the lead lifecycle. These tools are designed to execute core SDR tasks, such as enriching lead data, sending templated follow-up emails, or integrating with calendar systems to book discovery calls.
		- **Guardrails:** Guardrails act as a set of configurable rules and runtime checks that constrain the agent's behavior. Acts as a safety layer that can intercept prompts, validate the agent's proposed actions, and filter its final response to prevent harmful content, enforce business rules, and ensure the agent operates within its designated scope.
		- **Prompt templates:** Reusable templates that are dynamically populated with live CRM data via merge fields or semantic data from Data 360 RAG Retrievers. These templates allow agents to generate contextual, on-brand content while the Einstein Trust Layer securely masks sensitive information before the instructions are sent to the LLM.
- **Data 360**
	- Data 360 components, including DLOs, DMOs, vector store, and RAG retrievers, provide the agent with a unified view of all relevant enterprise data, from structured customer records to unstructured knowledge articles, ensuring responses are accurate and contextually grounded.
- **Sales Cloud**
	- **CRM data:** Connects the agent to the complete case history, providing crucial context on account details, contact records, and entitlements
		- **Schedule meeting between customer and SDR:** SDR Live Agent handoff can be configured to set up a live meeting using Task and Meeting Scheduling (Next Actions).
		- **Activity logging:** Capture events, tasks, and email activities, and relate it to leads, accounts, and opportunities as a result of SDR agent interactions.

**Interactions**

1. The customer sends and receives email through the channel, which routes to Agentforce.
2. Agentforce applies topics, actions, and guardrails to parse intent.
3. Agentforce drafts contextual responses using prompt templates enriched with CRM and Data 360 context.
4. A multi-turn email conversation continues until resolution or policy guidelines.
5. For qualified leads, Agentforce schedules a meeting and updates CRM.
6. If intent exceeds AI scope, Agentforce escalates to Sales Cloud SDR for a human service rep response.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Response Speed | <5 min first response (vs. 8–24 hrs) | Less personalized initial outreach when compared to phone |
| SDR Capacity | 2–5x increase in lead coverage | Loss of early relationship-building touchpoints |
| Qualification Consistency | Asynchronously acquire budget, authority, need, and timeline (BANT) coverage | May miss nuanced signals |
| Content Accuracy | RAG ensures up-to-date info | Requires curated sales product and enablement library. Multi-turn can be strenuous |
| Meeting Conversion | Significantly higher conversion | Some meetings with lower-quality leads if there are BANT gaps |
| Cost Efficiency | More cost-efficient than human SDR | Development and maintenance costs |

**Related Patterns**

[Answer Bot pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#answerbot-pattern): An effective pattern for self-service that uses generative AI to understand natural language for knowledge retrieval, and not just keywords

While the conversational agents in the previous section excel at reacting to user commands, proactive agents represent a paradigm shift: they act without being asked. This section provides the architectural patterns for building agents that autonomously monitor data and events originating both outside and within Salesforce.

**Problem**

Your organization generates critical business events within and outside Salesforce. There is trouble translating them into timely contextual action because they are scattered across applications and departments.

**Context**

- Your business processes span across several systems for CRM, payment processing, shipping, marketing automation, telemetry, and CDP.
- Your organization events occur 24/7, but your workforce availability is limited outside business hours. Systems are always on, but humans are not.
- The events lack context awareness—they miss customer context available in Salesforce, forcing multi-step conjoining of information. Today, implementation either exists as discrete complex automation or is performed manually.
- Humans act as a compiler to gather the data (in different formats) and *intelligently* react to disjointed events.
- Your target actions are applied to multiple systems.
![External event response pattern diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/external-event-response-pattern.png)

**Key Components**

- **Event source**
	- Data Action triggered events after external data has been ingested into Data 360
		- Third-party or Salesforce Heroku MCP servers capable of sending events to Salesforce via the Salesforce Pub/Sub API
		- External application capable of sending event notifications via the Salesforce Pub/Sub API
- **Optional middleware:** MuleSoft or Data 360 for transformations
- **Agentforce Agent:** The agent's behavior and purpose are defined by the following components.
	- **Topics and instructions:** Specifies the agent's core mission and its triggers, including defining its primary objective (for example, "Monitor all high-priority cases and prevent SLA breaches"). Contains the specific events or data conditions that the agent should listen for to initiate its tasks
		- **Actions:** Event-triggered and scheduled actions designed to respond to external events. While these actions operate autonomously for routine tasks, they often include the ability to orchestrate workflows that involve human intervention, escalating to users for review, approval, or handling scenarios that require human judgment.
		- **Guardrails:** Guardrails act as a set of configurable rules and runtime checks that constrain the agent's behavior. Acts as a safety layer that can intercept prompts, validate the agent's proposed actions, and filter its final response to prevent harmful content, enforce business rules, and ensure the agent operates within its designated scope.
		- **Prompt Templates:** Reusable templates that are dynamically populated with live CRM data via merge fields or semantic data from Data 360 RAG Retrievers. These templates allow agents to generate contextual, on-brand content while the Einstein Trust Layer securely masks sensitive information before the instructions are sent to the LLM.
- **Data 360**
	- Data 360 components, including **DLOs and DMOs,** that store event data [generated by external systems and sent to salesforce](https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-create-eventbusconnector-data-stream.html), transforming and building streaming or real-time insights
		- **Calculated, streaming, and real-time insights** supply agents with immediate, pertinent data regarding customers. This enables preemptive problem resolution, mitigating escalation. **Data graphs** proactively surface relationships and insights from disparate data sources, enabling early detection of patterns or anomalies relevant to the customer engagement, activity, and profile.
		- **Data 360 vector store and RAG** retrievers provide the agent with a unified view of all relevant enterprise data and unstructured knowledge articles, ensuring responses are accurate and contextually grounded.
- **Event targets**
	- Proactively notify employees or reach out to customers
		- Extensible to agents (see [Ambient Agent](#23-ambient-agent-patterns) and [Autonomous Agent](#25-autonomous-agent-patterns) patterns)

**Interactions**

1. A notable change occurs in the external system.
2. The external system emits an event and publishes it to Salesforce Event Bus via API (creates a platform event) or Pub/Sub API, or Event data is streamed to Data 360.
3. Subscribers of the event are triggered. A Flow is triggered.
4. The Flow calls [Agent Action](https://help.salesforce.com/s/articleView?id=platform.automate_flow_ref_elements_actions_generate_ai_agent_response.htm&type=5) with the event data. The agent determines the right course of action and executes it.
5. The outcome is a notification or a workflow being triggered. Notifications are delivered to a user in a collaboration tool (such as Slack). Tasks or events are also generated. Further, actions can call external systems. The events, therefore, are not lost but are proactively executed, signaled, and actioned, removing human overhead or complex automation to discover them.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Real-Time Integration | Events trigger actions within seconds. | API ingress complexity (partner SLA variability) |
| Intelligent Response | AI-powered decisions with CRM and external context | Enrichment adds latency and stale data (such as out-of-order events). |
| Loose Coupling | External systems independent of Salesforce logic | Async processing leads to eventual consistency. |
| Scalability | Handles burst events | API limits, event storage costs |
| Bidirectional | Salesforce can respond to external systems. | External API dependencies, failure scenarios |
| Security | Signed verified events, least (or zero) privilege access by external systems | Replay protection, key rotation, and operational overhead |

**Related Patterns**

[Judge & Jury pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#judge--jury-pattern): Can be used in conjunction with this pattern to ensure the accuracy and reliability of AI-powered decisions by leveraging multiple "juror" agents and a "judge" agent for congruence assessment

[Model of Models pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#model-of-models-pattern): This pattern embraces diverse viewpoints from multiple expert agents to generate richer insights, which can complement the proactive AI's intelligent responses.

**Problem**

Your organization's Salesforce ecosystem generates a constant stream of signals but has trouble translating them into timely contextual action, as they require business logic, governance, and humans to triage and act. Many times, the signals are lost without any action leading to lost opportunity.

**Context**

- Your organization uses one or more Salesforce clouds: Sales, Service, Marketing, Commerce, Health, Manufacturing, and others.
- You need intelligent triaging beyond simple routing or rule-based triaging. Your organization maintains hundreds of complex business rules.
- You require real-time or near-real-time response to events.
- Occasionally, your most privileged admins become the weakest link in the chain for not seeing the signals.
![Internal Salesforce platform event response pattern diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/internal-salesforce-platform-event-response-pattern.png)

**Key Components**

- **Event source layer**
	- CRM data, Platform Events, Change Data Capture (CDC) data, and Real-Time Event Monitoring (RTEM) data from low-level platform activity
- **Data 360**
	- Data 360 components, including **DLOs and DMOs,** that store event data [generated by CRM or platform events](https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-create-eventbusconnector-data-stream.html), transforming and building streaming or real-time insights
		- **Calculated, streaming, and real-time insights** supply agents with immediate, pertinent data regarding the customer, employee activity, or metadata changes in the system. This enables preemptive problem resolution, mitigating escalation. This real-time situational awareness empowers agents to deliver timely interventions for governance and compliance operational throughput.
		- **Data Graphs** proactively surface relationships and insights from disparate data sources, enabling early detection of patterns or anomalies relevant to the customer engagement, activity, and profile.
		- **Data 360 vector store and RAG** retrievers provide the agent with a unified view of all relevant enterprise data and unstructured knowledge articles, ensuring responses are accurate and contextually grounded.
- **Agentforce Agent:** The agent's behavior and purpose are defined by the following components.
	- **Topics and instructions:** Specifies the agent's mission to enforce business rules and automate processes based on data changes within Salesforce. It defines the agent's objective (for example, "Ensure all opportunities are updated with a primary contact before reaching the negotiation stage") and the specific record creations, field updates, and so on that trigger the agent.
		- **Actions:** Event-triggered and scheduled actions designed to respond to internal Salesforce events. While these actions operate autonomously for routine tasks, they often include the ability to orchestrate workflows that involve human intervention, escalating to users for review, approval, or handling scenarios that require human judgment.
		- **Guardrails:** Guardrails act as a set of configurable rules and runtime checks that constrain the agent's behavior. Acts as a safety layer that can intercept prompts, validate the agent's proposed actions, and filter its final response to prevent harmful content, enforce business rules, and ensure the agent operates within its designated scope.
		- **Prompt Templates:** Reusable templates that are dynamically populated with live CRM data via merge fields or semantic data from Data 360 RAG Retrievers. These templates allow agents to generate contextual, on-brand content while the Einstein Trust Layer securely masks sensitive information before the instructions are sent to the LLM.
- **Event targets**
	- Proactively notify employees or reach out to customers.
		- Extensible to call other agents (see [ambient AI](#23-ambient-agent-patterns) and [autonomous AI](#25-autonomous-agent-patterns) patterns)

**Interactions**

1. A notable change occurs within the internal system, such as an update to a CRM record, a metadata modification, or a data action triggered from Data 360.
2. The internal system emits an event and publishes it to Salesforce Event Bus via API (creates a platform event) or Pub/Sub API, or event data is streamed to Data 360.
3. Subscribers of the event are triggered and activate a Flow or Apex.
4. The activated Flow or Apex calls [Agent Action](https://help.salesforce.com/s/articleView?id=platform.automate_flow_ref_elements_actions_generate_ai_agent_response.htm&type=5).
5. The outcome is a notification or a workflow being triggered. Notifications are delivered to a user in a collaboration tool (such as Slack). Tasks or events are also generated. Further, actions can call external systems.
6. The events, therefore, are not lost but are proactively executed, signaled, and actioned, removing human overhead or complex automation to discover them.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Real-Time Integration | Events trigger actions within seconds. | More layers may cause latency for simple event handling. |
| Intelligent Response | AI-powered decisions with CRM and external context | Enrichment adds latency and stale data (for example, out-of-order events). |
| Loose Coupling | Fan out (more subscribers) and extensible | Async processing leads to eventual consistency across subscribers. |
| Scalability | Handle burst events | API limits |
| Security | Platform-provided Trust layer | Non-negotiable operational overhead |

**Related Patterns**

[Listener/Feed pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#listenerfeed-pattern): Can be combined with the Listener pattern to trigger proactive actions based on internal Salesforce events

[Data Steward pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#data-steward-pattern): Proactive AI can utilize data stewards to ensure data quality and consistency when responding to internal events

[Zen Data Gardener pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#zen-data-gardener-pattern): For scheduled, proactive data grooming and standardization triggered by internal events or at regular intervals

We began with agents that respond interactively in a conversation channel and then progressed to agents that react to specific events. Moving beyond the event-driven model of proactive agents, ambient agents represent a paradigm shift from direct interaction to proactive, background assistance. These are headless agents that observe the digital environment in the background. They act as the "eyes and ears" of the system, perceiving context from user activity or data streams and then coordinating with other agents or humans to complete tasks, surface insights, or provide guidance.

**Problem**

Your organization's business activities generate continuous streams of valuable information (calls, meetings, chats, sensor data, and more), but this data disappears in real time without capture or analysis. By the time humans manually document these interactions, critical insights are lost and the moment for timely intervention has passed. Organizations miss the majority of actionable intelligence **needed in real time** and buried in ephemeral streams, leading to gaps, lost coaching opportunities, and decisions made without complete context.

**Context**

- Your business activities generate continuous streams from various sources, including voice and video meetings, live chats, sensor telemetry, screen activity, and transactional data.
- You require real-time or near-real-time insights (within seconds or minutes, and not hours or days) to effectively respond to and act upon these streams.
- Manual documentation processes are failing, characterized by low compliance and refresh rates, high cognitive burden on employees, and incomplete capture of critical information.
- You need multi-modal understanding, combining data from audio, video, screen share, chat, and other metadata to create a complete and accurate context of interactions and events.
- You require both immediate analysis for real-time coaching and alerts and historical analysis for post-interaction summaries and long-term trend identification.
- Temporal context (episodic memory) is crucial for your analysis, including understanding the sequence, timing, transitions, and patterns across various time windows within your data streams.

**Key Components**

- **Stream source**
	- Voice and video: Video conferencing tools (like Slack Huddle, Zoom, Google Meet, and Microsoft Teams) and telephone systems
		- Collaboration tools: Slack, Teams, and others
- **Stream capture connectors**
	- Native SDK: Vendor-provided SDK that helps retrieve transcripts or messages that support real-time stream segments or transcripts
- **(Optional) Stream processing layer**
	- For audio streams, if transcripts are not available real time, a speech-to-text capability that translates audio to text. You can also use a managed provider like Amazon Transcribe.
		- For other data streams, optionally, a stream processing engine like Data 360 or Apache Flink
- **Data 360**
	- Data 360 components, including **DLOs and DMOs,** that store event data, transforming and building [streaming or realtime insights](https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-create-eventbusconnector-data-stream.html)
		- **Calculated, streaming, and real-time insights** supply agents with immediate, pertinent data regarding customers, their activity, and critical insights. This enables preemptive problem resolution, mitigating escalation. This real-time situational awareness empowers agents to deliver timely interventions and personalized support to employees, thereby optimizing customer satisfaction and operational throughput.
		- Data 360 components, including **DLOs and DMOs,** that store customer data, transforming and building real-time insights
		- **Data 360 vector store and RAG** retrievers provide the agent with a unified view of all relevant enterprise data and unstructured knowledge articles, ensuring responses are accurate and contextually grounded.
- **Agentforce Agents.** This pattern focuses on an ambient agent that observes a continuous data stream, such as a live call transcript or a video feed. It acts as a real-time listener, interpreting unstructured data as it happens. For example, an agent listening to a live call might invoke a Data Discovery agent to enrich a lead's record based on new context shared in the conversation. Here is an example of such a headless agent:
	- **Feedback Agent.** The agent's behavior and purpose are defined by the following components.
		- **Topics and instructions:** Defines the agent's primary mission to analyze conversational streams and extract structured feedback and performance metrics. This includes instructions to monitor for customer sentiment, identify mentions of key products or competitors, and assess whether the human agent is adhering to company best practices or a sales playbook.
				- **Actions:** Actions to transform unstructured conversational data into actionable business intelligence. These actions enable the agent to create a "Feedback Summary" record, log product feature requests, flag calls with negative sentiment for manager review, and update a dashboard to track overall agent performance against key metrics.
				- **Guardrails:** Guardrails act as a set of configurable rules and runtime checks that constrain the agent's behavior. Acts as a safety layer that can intercept prompts, validate the agent's proposed actions, and filter its final response to prevent harmful content, enforce business rules, and ensure the agent operates within its designated scope.
				- **Prompt Templates:** Structured, templated LLM instructions that can receive input and provide an LLM-generated output
- **Ambience targets**
	- Notify users on the surface where the agent and user are, such as in a video call or a desktop application

**Interactions**

1. When a stream is activated (such as when a user joins the video call), the agent attaches itself as an observer.
2. The agent starts to receive stream data, incrementally detects intents, makes decisions, and calls actions.
3. The agent contextualizes based on intent and fetches additional data (structured or unstructured).
4. The agent provides just-in-time real-time responses without user prompting: it can detect an objection in a sales call and provide important information to handle the objection.
5. Agents can compile a consolidated summary and actions and share them with other agents and users.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Window Size | Small window—lower latency, faster coaching | Also has less context, lower accuracy |
| Processing Mode | Real-time presents an immediate assistant opportunity. | Resource intensive |
| Stream Resolution | High quality audio and video can have better accuracy but increase latency. | More storage and compute |
| Retention Period | Vast amounts of data can be used for training and compliance. | More storage costs, can lead to noise |
| Multi-Modal | Richer context, holistic understanding | Sync complexity |
| Ambience | Can provide consistent support to the human user | Privacy/policy enforcement |

**Related Patterns**

[Listener/Feed pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#listenerfeed-pattern): Can be combined with the Listener pattern to process real-time streams of conversation and user interaction data and surface relevant context and insights

[Interrogator pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#interrogator-pattern): Can be used in conjunction with this pattern to assemble context from multiple sources within the stream and answer questions

**Problem**

Your employees perform hundreds of business-critical activities daily across email, calendar, calls, and applications, yet these activities remain invisible to organizational systems until they are manually logged—which rarely happens. This activity blindness means CRM data is incomplete, AI models lack the signals needed for intelligent recommendations, and managers have no real-time visibility into customer engagement. Manual activity logging creates a productivity tax while still missing most of the actual work.

**Context**

Just like the stream observer, this is a data and content observer that provides actionable tasks or performs actions on behalf of the user.

**Key Components**

- **Data layer**
	- **CRM data**: Customer data available in CRM that provides context to the agent (for example, when the user is on an Opportunity page, the agent can retrieve information about the opportunity and the associated account from CRM).
		- Data 360 components, including **DLOs and DMOs,** that store relevant customer data ingested from different sources
		- **Calculated, streaming, and real-time insights** supply agents with immediate, pertinent data regarding customers, their activity, and critical insights. This enables preemptive problem resolution, mitigating escalation.
		- **Data 360 vector store and RAG** retrievers provide the agent with a unified view of all relevant enterprise data and unstructured knowledge.
- **Agentforce Agent:** This pattern focuses on an ambient agent that observes a user's actions directly within the UI. It acts as a real-time assistant, understanding the context of the user's workflow to provide guidance. For example, an agent might monitor a service representative filling out a case record and proactively surface a relevant knowledge article. Here is an example of such a headless agent:
	- **Feedback Agent.** The agent's behavior and purpose are defined by the following components.
		- **Topics and instructions:** Defines the agent's mission to monitor a user's actions within the UI and provide contextual assistance. This includes its objective (for example, "Guide a service rep through the case resolution process") and the specific UI events or data entry patterns it should watch for to proactively offer help.
				- **Actions:** Actions, built using Apex or Flow, to surface relevant information and next best actions directly within the user's workflow. These actions enable the agent to fetch and display a relevant knowledge article, suggest a valid next step in a process, or flag a data entry field that may violate a business rule, all in response to the user's real-time activity.
				- **Guardrails:** Guardrails act as a set of configurable rules and runtime checks that constrain the agent's behavior. Acts as a safety layer that can intercept prompts, validate the agent's proposed actions, and filter its final response to prevent harmful content, enforce business rules, and ensure the agent operates within its designated scope.
				- **Prompt templates:** Reusable templates that are dynamically populated with live CRM data via merge fields or semantic data from Data 360 RAG Retrievers. These templates allow agents to generate contextual, on-brand content while the Einstein Trust Layer securely masks sensitive information before the instructions are sent to the LLM.
- **Ambience targets**
	- Notify users on the surface where the agent and user are, such as on a web page or an admin page

**Interactions**

1. When a user visits a page or app, the agent attaches itself as an observer.
2. The agent starts to inspect data and actions, incrementally detects intents, makes decisions, and calls actions.
3. The agent contextualizes based on intent and fetches additional data (structured or unstructured).
4. The agent provides just-in-time real-time responses without user prompting and can suggest next best actions or offer to perform them on behalf of the user.
5. Agents can seamlessly share this with other agents and users.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Scope | Wide set of activity coverage, agent can share the context in different modals (email, calendars, app pages) | Computation cost |
| Intelligent Automation | Can be a module and extend to fully autonomous AI and can eliminate humans out of the loop where policy is clear | More agent evaluation. Risk of false positives or errors, can go undetected in a reasonable timeframe |
| Interception Complexity | Can benefit from real time analytics. For example, can detect fraud or threat and stop transactions from occurring | Need agent and human workflows synchronized |
| Context Depth | Deeper context leads to intelligent decisions | Need to be context-complete |
| Agent Autonomy | Headless agents work in the background without user prompting, so reduces friction | Less transparency into agent decision-making, more audit trails |
| Multi-agent | Headless agents can work together to form specialized agents | Headless orchestration and additional complexity |

**Related Patterns**

[Listener/Feed pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#listenerfeed-pattern): Can be combined with the Listener pattern to trigger proactive actions based on observed activity

[Data Steward pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#data-steward-pattern): Activity interception AI can utilize data stewards to ensure data quality and consistency when logging intercepted activities.

[Generator pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#generator-pattern): Can be used to automatically generate activity summaries or follow-up tasks based on intercepted activities

This section details patterns for collaborative agents, where one or more agents work in concert with a human user to achieve a shared goal. These recipes focus on creating a seamless partnership: agents handle complex data gathering and task execution while keeping the human in the loop for decisions, approvals, and strategic guidance.

In this model, agents handle the automatable parts of a workflow. The process becomes a dynamic feedback loop.

- A human might initiate a task through a Conversational Agent, which triggers a Proactive Agent to manage the backend steps.
- Concurrently, an Ambient Agent might observe their actions to provide real-time guidance.

This process creates a seamless fusion of human and digital labor. This pattern showcases how Agentforce facilitates a multi-agent, human-in-the-loop system to tackle complex jobs that no single agent—or human—could manage alone.

**Problem**

Your business processes require collaboration among workers from different organizations— both internal and external— each with distinct jobs to be done involving different skills and priority. Process bottlenecks can occur anytime and anywhere due to resource capacity, skill constraints, or due to the amount of information exchanged.

**Context**

- Processes span across teams and need multiple team members to collaborate for a successful outcome.
- Agent assistants already help your workforce in one-to-one scenarios as conversational, proactive, and ambient agents.
- Processes use agents in appropriate segments of your business processes. However, processes also need human–agent collaboration. This collaboration may involve human-to-human with assistance by agents or human—agent—human collaboration.
- Skill gaps are filled by agents.
- Agents help improve collaboration by reducing human effort in tasks such as follow-ups and exchanging critical information to aid decision-making.
- Agents can also collaborate and delegate based on policies and guidelines.

**Key Components**

- **Collaboration surface**  
	Agentic collaboration requires a shared space where all participants, both humans and agents, can interact. These collaboration surfaces are no longer static, human-only environments. Instead, they are channels where agents can be invited to join, contribute, and even initiate conversations, fundamentally changing the nature of teamwork. For example, an agent can create and initiate a case swarm in Slack inviting human subject matter experts and other agents to collaborate on the case.
- **Agentforce Agents**  
	This pattern moves beyond individual agent patterns to demonstrate how they converge in a Collaborative Agent model, orchestrating complex processes that intelligently augment human capabilities. The preceding patterns—Conversational (2.1), Proactive (2.2), and Ambient (2.3) - define the Agentforce Agent components.c direction. A **Conversational Agent** acts as the primary interface, working alongside the human and acts as the interface between humans and all agents involved in the collaboration. When a task is too multifaceted the conversational agent initiates a collaborative session, bringing together the human users and the necessary headless agents to work on the problem concurrently. The process becomes a dynamic feedback loop where a human might initiate a task, which then triggers a **Proactive Agent** to manage the backend steps, while an **Ambient Agent** might observe to provide real-time guidance, creating a seamless fusion of human and digital labor.
- **Data Layer**  
	In the collaborative agent model, the data layer serves a more dynamic role than simply providing information; it becomes the persistent memory and shared workspace for the entire human-agent team. While each agent involved has its own specific data needs, as defined in its respective pattern, their collaboration on a complex task hinges on a shared data foundation that tracks the state of the overall job.
	This shared state is crucial. As a task is handed off from a conversational agent to a proactive agent, and then to a human for approval, the data layer must track the progress, context, and decisions made at each step. This ensures that every participant has a consistent and up-to-date view of the episode.

**Interactions**

1. Humans initiate a collaborative session with other humans and agents.
2. Context, goals, jobs, and outcomes are defined.
3. The agent enriches the context by bringing in additional information and proactively plans the steps required to complete the job, along with owners who are humans or agents.
4. Progress is observed, context is updated, and actions are performed.
5. Where agents perform the job, the agent provides detailed information to help human stakeholders understand reasoning, provide feedback, and allow interceptions.
6. Agents complete the work with full transparency and compliance.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Native Collaboration Surfaces | Agents can participate and immediately contribute to human flow of work | User adoption requires additional training and enablement |
| Bidirectional context sharing | Agents can surface and share context with all parties, making information available to all. | Intentional asymmetric sensitive information requires additional safeguards. |
| Collaboration | Agents enable real-time collaboration, delivering immediate feedback and faster resolution time. | Faster resolutions means more active work in the queue for humans potentially leading to fatigue |
| Specialization | Domain specific agents offer high-value assistance. | Increased bounded context needs and domain specificity. Complexity to adapt to changes |
| Observability | Provide reasoning, audit trails, Agent Evaluations build trust | Increased telemetry costs |

**Related Patterns**

[Operator pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#operator-pattern): Collaborative agents often act as operators, routing requests to the appropriate specialist AI agents or human service reps and negotiating intent.

[Orchestrator pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#orchestrator-pattern): In scenarios involving collaboration, an orchestrator agent manages a swarm of AI agents, aggregating their responses for a seamless user experience.

[Workspace (Radar O'Reilly) pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#workspace-radar-oreilly-pattern): Collaborative agents use this pattern to manage a responsive, single-pane-of-glass UX, updating relevant content in real-time within a conversation flow.

In contrast to collaborative patterns that assist a user, autonomous agents are designed for full delegation. This section provides the architectural blueprints for agents that can independently plan and execute complex, multi-step tasks to achieve a high-level goal without requiring human intervention. The focus here is on creating a system you can task with an objective and trust to carry it out from start to finish.

**Problem**

Your organization realizes value through a highly complex set of processes, each with distinct policy-driven jobs, playbooks, and specific skills needed for execution. These are often programs that require significant investment of time and resources.

Setting up a new program has high overhead and can take months before realizing value. Implementing feedback and improvements often requires additional time and effort. Complexity is primarily driven by your organization's structure, where distributed applications and processes can cause dependencies requiring humans to manage the program.

**Context**

- Agents can operate independently from start to finish. Agents are designed and configured so the goal, plan, and strategy are preestablished.
- Agents can make all decisions without seeking human approval. Agents are provided with policy and compliance guidelines.
- Agents can access the necessary context and data it needs and can perform necessary actions without needing humans.
- Humans are notified but are not "in the loop."

**Key Components**

- **Goal and strategy definition layer**
	- **Process playbooks:** Detailed descriptions of autonomous execution with deterministic rules that agents must follow
		- **Autonomous decision criteria:** Rules that enable agents to make decisions without requiring human approval
		- **Fallback rules:** Predefined actions for handling default or exception scenarios when an agent's primary process fails
		- **Scopes:** Clearly defined boundaries outlining what agents can and cannot do, including how out-of-scope situations must be handled
		- **Success criteria and definition of done:** The metrics and conditions that determine when an agent's task is successfully completed
- **Agentforce Agents**
	- **Agent orchestrator or choreographer:** The principal agent that owns the goal, reasons, and plans execution
		- **Topics and instructions**: Once a goal is defined, the orchestrator or choreographer agent takes the lead in breaking down that overarching objective into smaller, manageable jobs or sub-tasks. It devises a comprehensive plan, outlining the sequence of jobs and identifies the specific agents or tools required for each step. Finally, the orchestrator agent ensures the seamless execution of the plan, monitoring progress, managing dependencies, and making adjustments as needed to achieve the goal efficiently and effectively. In the case of a choreographer agent, it passes the context and state to the downstream agents to carry the job through to completion.
				- **Actions:** Actions call tools to perform a function, retrieve data, or delegate to other headless agents, enabling a broader range of capabilities and more complex workflows.
				- **Guardrails:** Guardrails act as a set of configurable rules and runtime checks that constrain the agent's behavior. Acts as a safety layer that can intercept prompts, validate the agent's proposed actions, and filter its final response to prevent harmful content, enforce business rules, and ensure the agent operates within its designated scope.
- **Data Layer**
	- **CRM Data:** Customer data available in CRM that provides context to one or more agents
		- Data 360 components, including **DLOs and DMOs,** that store relevant customer data ingested from different sources
		- **Calculated, streaming, and real-time insights** supply agents with immediate, pertinent data regarding customers, their activity, and critical insights. This enables preemptive problem resolution (like handling email bounces), mitigating escalation.
		- **Data 360 vector store and RAG** retrievers provide the agent with a unified view of all relevant enterprise data and unstructured knowledge
		- **Slack channel message or conversation data** such as case history and conversational agent history that provide conversation context
- **Monitoring and oversight**
	- **Agent goal progress monitoring:** Tracks the progress of autonomous agent sessions to measure outcomes and ensure alignment with objectives
		- **Agent operations monitoring:** Tracks the real-time status of autonomous agents for intervention and troubleshooting, ensuring smooth operation
		- **Agent governance monitoring:** Tracks trace and audit logs to ensure autonomous agents comply with predefined goals, objectives, and ethical guidelines

**Interactions**

1. The job is defined with clear outcomes.
2. The job is initiated through one of the following methods:
	- An agent is tasked.
		- An agent proactively picks up the job based on qualifications.
		- An agent performs the job in the background.
3. The agent clearly establishes expectations and informs humans, detailing the goal, plan, and strategy. The plan details step-by-step processes, agents used, data used, scope, agent evaluation plan, and checkpoints for humans to monitor progress, operations, and governance.
4. The agent begins execution. At each milestone, it updates the state and progress. Humans have the ability to provide feedback or intercept the agents as needed.
5. The agent completes the job. The outcome and results are available in the monitoring dashboard.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Speed | Agents complete the tasks in hours to days rather than weeks to months | Requires enablement for autonomous agentic operation |
| Autonomy | Agents achieve full execution without human intervention | Intervention is limited and costly during execution |
| Scalability | Agents scale easily | Rate limits must be established to prevent locking of resources. |
| Consistency | Agents adhere to policies via guardrails | New scenario handling requires inspection to ensure the correct outcome. |
| Cost | Agents avoid human in the loop | The process is expensive to build |
| Human resources | Agents free up critical and expert resources | Experts lack experiential visibility through doing, reducing ability to identify process improvements |
| Quality control | Can monitor and review | Remediation costs are high if agent errors are not caught immediately |
| Accuracy | Agents can use context and policies to make the right decision. | Context and data must be curated and maintained to remove any ambiguity or staleness. |

**Related Patterns**

[Project Manager pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#project-manager-pattern): Autonomous agents often embody this pattern, overseeing long-running, multi-step processes from initiation to completion with minimal human intervention.

[Configurer pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#configurer-pattern): Autonomous agents can use this pattern to automatically generate and validate configurations based on natural language requirements or predefined policies, ensuring compliance and accuracy without manual oversight.

[Zen Data Gardener pattern](https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture#zen-data-gardener-pattern): This pattern can be used by autonomous agents for scheduled, background data grooming and standardization, ensuring data quality and consistency over time to support accurate agent decision-making.

Now, we will bring the agent taxonomy and agent patterns to life by exploring how they are implemented on the Salesforce Platform. For those unfamiliar with the core components of Agentforce, the [Appendix](#appendix) provides a helpful refresher on the key technologies referenced throughout this chapter and the next.

This section takes the taxonomy of agents and illustrates each one with a common use case to show how they are used in real-world applications.

A customer, Jane, visits a company's website to check the status of her recent order.

- **Interaction:** Jane opens the chat window (the Agentforce Chat Client).
- **Agent Action:** The conversational agent greets her and asks how it can help. Jane asks, "Where is my latest order?"
- **Process:**
	1. The agent, grounded with Jane's customer information from Salesforce, identifies her most recent order.
		2. It queries the shipping system (via a MuleSoft connector) for the latest tracking information and provides Jane with a real-time update and a tracking link.
		3. It then looks up the policy and automatically upgrades to expedited shipping.
		4. When Jane asks a complex question the agent can't handle, it seamlessly escalates the chat to a human service agent, providing the full transcript for context.

**Recipe**

Patterns used: [Conversational AI pattern](#21-conversational-agent-patterns), [Integrating transactional data to agents](#42-data-integration-patterns)

**Design Time**

1. Set up a conversational agent.
	| Set up Enhanced Chat | → | Create Service agent | → | Define Support Orders topic | → | Create Get Order action |
	| --- | --- | --- | --- | --- | --- | --- |
	|  |  |  |  |  |  | ↓ |
	| Add outbound escalation Omni-Channel flow | ← | Create Escalate topic | ← | Add actions to topics | ← | Create Get Status action |
	| ↓ |  |  |  |  |  |  |
	| Publish the agent |  |  |  |  |  |  |
2. [Set up Enhanced Chat](https://help.salesforce.com/s/articleView?id=service.miaw_setup_stages.htm&type=5) as Jane's chat entry point so she can open the Agentforce window in the web page.
3. Enable Agentforce and [create a Service Agent](https://help.salesforce.com/s/articleView?id=ai.service_agent_setup.htm&language=en_US&type=5) in Agentforce Builder to handle conversations and trigger custom actions.
4. Define a Support Orders [topic](https://help.salesforce.com/s/articleView?id=ai.copilot_topics.htm&type=5) with a description and [instructions](https://help.salesforce.com/s/articleView?id=ai.copilot_actions_instructions.htm&type=5) so the agent naturally recognizes "Where is my latest order?".
	1. [Create custom agent actions](https://help.salesforce.com/s/articleView?id=ai.copilot_actions_custom.htm&type=5):
		1. Get Latest Order for Contact action to retrieve Jane's most recent order
				2. Get Shipping Status by Order ID [action](https://help.salesforce.com/s/articleView?id=ai.copilot_actions.htm&type=5) to fetch tracking information via MuleSoft
				3. Optionally orchestrate both actions in Flow—fetching the latest order and calling MuleSoft— [using external service actions](https://help.salesforce.com/s/articleView?id=platform.enhanced_external_services_example_create_flow.htm&type=5).
				4. Add both actions to the Service Agent in the [builder](https://help.salesforce.com/s/articleView?id=ai.agent_builder_explore.htm&type=5), link them to the Orders & Tracking topic, and publish.
5. Define an Escalation topic with a description to escalate to a service rep.
	- Create and activate an outbound Omni-Channel flow.
		- Add it to the Connections tab in the builder for escalation with an escalation message.
6. Set up Omni-Channel.
	| Configure Omni-Channel | → | Define escalation rules in instructions | → | Set priorities and capacity | → | Test and validate |
	| --- | --- | --- | --- | --- | --- | --- |
7. Enable seamless escalation to human service agents when the AI agent cannot resolve the query. Configure Omni-Channel routing to assign chats to service reps and [transfer the full transcript](https://help.salesforce.com/s/articleView?id=service.live_agent_transfer_chat_about.htm&type=5) for context.
8. Integrate escalation logic into the Agentforce instructions and an escalation action so the agent knows when to transfer complex cases. Manage [routing priorities and capacity](https://help.salesforce.com/s/articleView?id=service.console_lex_service_setup_omnichannel.htm&type=5) through [Omni Supervisor](https://help.salesforce.com/s/articleView?id=service.omnichannel_set_up_supervisors.htm&type=5).
9. [Test](https://help.salesforce.com/s/articleView?id=ai.agent_testing_center.htm&type=5) the full experience: Jane opens the chat, and the agent greets her, identifies her order, retrieves shipping data, and escalates seamlessly when human intervention is required (see also [Enable Enhanced Event Logs](https://help.salesforce.com/s/articleView?id=ai.copilot_setup_enhanced_event_logs.htm&type=5)).
10. Set up data integration.
	| Map context data | → | Create MuleSoft API credentials | → | Register MuleSoft external service |
	| --- | --- | --- | --- | --- |
11. Ground the agent with Jane's Salesforce context by [mapping her contact and order records](https://help.salesforce.com/s/articleView?id=ai.service_agent_context_variables.htm&type=5) through authenticated chat or pre-chat forms.
12. Connect Salesforce securely to the MuleSoft shipping API using [external credentials and named credentials](https://help.salesforce.com/s/articleView?id=platform.external_services_define_named_credential.htm&type=5) for authentication.
13. If MuleSoft exposes an OpenAPI specification, [register it as an external service](https://help.salesforce.com/s/articleView?id=platform.external_services_register.htm&type=5) so Flow and the agent can call it declaratively.
14. Set up unstructured data integration.
	1. [Create a new data library](https://help.salesforce.com/s/articleView?id=ai.data_library_setup.htm&type=5) from Setup. Name it "Order and Shipping Policy."
		2. Add the PDFs of policy documents that contain the shipping policy exceptions.
		3. Behind the scenes, the documents are automatically chunked, indexed, and made ready to use.

**Agent Runtime Process Flow**

Once the agent is set up and deployed, the following sequence of steps occurs at runtime.

1. **Chat launch:** Jane opens the Agentforce chat (embedded service). Session and contact context load after Jane is logged in.
2. **Greeting and intent:** The agent greets Jane. Jane asks for the status of an order, and intent detection maps "latest order" to the Orders & Tracking topic.
3. **CRM lookup:** The agent triggers the Get Latest Order action and queries Salesforce (order summary/orders) for Jane's most recent record.
4. **Shipping query:** The agent calls the MuleSoft API via a named credential, and /shipping/status/{orderId} returns a real-time status and a tracking URL.
5. **Response composition:** Agentforce merges results and composes a response: "Your order \[OrderID\] shipped via \[Carrier\], arriving tomorrow — \[Track Here\]."
6. **Fallbacks:** If there is no match or an API failure, the agent apologizes and offers to retry to fix any data issues.
7. **Escalation:** Complex or emotional queries automatically transfer to a human via Omni-Channel, passing on the full chat and context.
8. **Logging:** All intents, actions, and outcomes are stored in interaction logs. API latency is monitored in Anypoint Monitoring.
9. **Continuous improvement:** Escalations feed Agentforce retraining; common flows are refined in the subsequent release.

A high-value customer, John, has added over $1,000 worth of products to his online cart but doesn't complete the purchase within 60 minutes.

- **Trigger:** A Salesforce Platform event, Cart\_Abandoned\_\_e, is fired from the ecommerce system, containing John's contact ID and the cart value.
- **Agent Action:** A proactive agent, subscribed to this event, immediately springs into action.
- **Process:**
	1. The agent checks John's record in Salesforce and sees he is a VIP customer.
		2. It creates a high-priority task for John's account manager, Sarah, with all the details of the abandoned cart.
		3. It sends a notification to Sarah via Slack, urging her to follow up.
		4. Simultaneously, it enrolls John in a targeted Marketing Cloud journey that sends a reminder email with a limited-time 10% discount code to encourage him to complete the purchase.

**Recipe**

This recipe details the implementation of a proactive AI agent on the Salesforce Platform to address high-value cart abandonment by VIP customers. The solution leverages Salesforce Platform Events, Data 360 for knowledge retrieval, and Agentforce to orchestrate timely and intelligent follow-up actions, thereby transforming passive data into active business engagement.

**Design Time**

1. Set up an abandoned cart event to trigger when John, a VIP customer, leaves the cart abandoned.
	| Create custom Contact field | → | Define new platform event |
	| --- | --- | --- |
	1. Create a Cart\_Abandoned\_\_e platform event with the [fields](https://developer.salesforce.com/docs/atlas.en-us.platform_events.meta/platform_events/platform_events_define_ui.htm) Contact Id, Cart Value, Cart Last Updated DateTime, and Cart Details.
		2. Configure the abandonment event: Using Commerce Cloud, [create a platform event](https://developer.salesforce.com/docs/commerce/salesforce-commerce/guide/b2b-b2c-comm-notifications-platform-event.html) for checkout event notifications. Abandonment is detected when the cart checkout session state is in an intermediate state and the session times out after a threshold. Alternatively, if your ecommerce is an external system, publish the event to Salesforce using [any of these methods](https://developer.salesforce.com/docs/atlas.en-us.platform_events.meta/platform_events/platform_events_publish.htm): Flows, Apex, Salesforce APIs, or Pub/Sub API.
		3. In the Contact object, create a new field, Customer\_Tier\_\_c, with the picklist values Standard, Premium, and VIP.
2. Set up unstructured data ingestion in Data 360: Add a discount policy document sourced from a document repository to [Data 360 via Amazon S3](https://developer.salesforce.com/docs/data/data-cloud-int/guide/c360-a-awss3-connector.html).
	| Create AWS S3 credentials | → | Create new S3 Data Stream | → | Configure and deploy stream | → | Create Search Index |
	| --- | --- | --- | --- | --- | --- | --- |
	|  |  |  |  |  |  | ↓ |
	|  |  |  |  | Test retrieval function | ← | Configure and deploy index |
	1. Create external credentials to access S3: Create a new set of access keys and secrets for an IAM user or IAM Amazon Resource Name (ARN) for an IdP.
		2. Create a new S3 data stream: On the Data Streams tab, create the data stream Policy Documents Stream, select the S3 source, choose the PDF file type, set the refresh frequency, map the metadata fields (file name and size), and then deploy.
		3. After the data stream is complete, create a search index: Use passage extraction for chunking, the [E5-large-v2 embedding model](https://help.salesforce.com/s/articleView?id=data.c360_a_search_index_reference.htm&type=5), and the hybrid search type, and then deploy the index.
		4. Test the created retrieval function.
3. Set up the VIP Cart Recovery agent.
	| Create agent from template | → | Add Recover VIP Cart topic | → | Add topic instructions | → | Create Slack alert action |
	| --- | --- | --- | --- | --- | --- | --- |
	|  |  |  |  |  |  | ↓ |
	| Add actions to topic | ← | Create journey enrollment action | ← | Create discount offer action | ← | Create cart recovery task |
	1. Create an agent from the [Agentforce Employee Agent template](https://help.salesforce.com/s/articleView?id=ai.agent_employee_agent_setup.htm&type=5).
		2. Add a new topic, Recover VIP Cart, with the description that this agent handles high-value cart abandonment for VIP customers.
		3. Add topic instructions to validate VIP status, qualify the cart, notify the account manager in Slack, recommend a discount offer, and enroll the customer in the cart recovery email journey.
		4. Create actions and a task.
		- Alert Account Manager action: Sends a proactive Slack notification
				- Recover Abandoned Cart task, assigned to the manager with cart details
				- Get Discount Offer action: Analyzes policy and previous purchase history. Create a prompt template with grounding, reference the retrieval function in the prompt template, and use the data.
				- Enroll in Recovery Journey action: Enrolls in the Marketing Cloud recovery journey [via the API](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html) and takes in all subscriber data and the discounted offer email message generated from the agent.
		5. Add the actions to the topic.
		6. Create a VIP customer cart recovery journey [using templates](https://help.salesforce.com/s/articleView?id=sf.mc_jb_use_journey_builder_template.htm&language=en_US&type=5) in Marketing Cloud, or [create a new journey](https://help.salesforce.com/s/articleView?id=mktg.mc_jb_create_multistep_journey.htm&type=5).
4. Wire a platform event to call the agent.
	| Create event-triggered flow | → | Subscribe to platform event | → | Add agent invocable action | → | Pass event data to agent |
	| --- | --- | --- | --- | --- | --- | --- |
	1. Create a new platform-event-triggered flow, VIP Cart Abandonment Recovery.
		2. Select the Cart Abandoned event the flow should subscribe to.
		3. [Set up a custom agent](https://help.salesforce.com/s/articleView?id=ai.agent_custom_invocable_action_flow_set_up.htm&type=5) invocable action in Flow Builder, and select the VIP Cart Recovery agent. Send the request to initiate a VIP abandoned cart recovery for the customer and send the platform event payload.

**Agent Runtime Process Flow**

Once the agent is set up and deployed, the following sequence of steps occurs at runtime.

| Customer abandons cart | → | Commerce Cloud publishes event | → | Platform event triggers Flow | → | Flow invokes Employee Agent |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  | ↓ |
| Analyzes for discount offer | ← | Creates task for manager | ← | Alerts manager in Slack | ← | Agent executes Recovery topic |
| ↓ |  |  |  |  |  |  |
| Enrolls customer in journey | → | Customer redeems the offer | → | Agent analyzes outcome for feedback |  |  |

1. **Cart abandonment detection:** John adds $1,200 to his cart, and no checkout or stage progression after 60 minutes triggers abandonment.
2. **Platform event publication:** Commerce Cloud publishes the Cart\_Abandoned\_\_e event with John's contact ID, cart value of $1,200, cart modified date, and other details.
3. **Flow initialization:** The platform event triggers the VIP Cart Abandonment Recovery Flow.
4. **Employee Agent activation:** When the Flow runs, the VIP Cart Recovery agent gets invoked.
5. **Topic execution:** The agent resolves to the Recover VIP Cart topic and executes the instructions.
6. **Notification creation:** The agent alerts John's account manager Sarah in Slack.
7. **Task creation:** The agent creates a task for Sarah, advising her of the follow-ups it will perform.
8. **Discount analysis:** The agent runs the discount analysis by calling the Data 360 retriever function to ask for "max allowed discounts" based on the cart value, customer tier, and purchase history. In this case, the function recommends a discount offer of 10%.
9. **Email preparation and journey enrollment:** The agent prepares a discount offer email and enrolls John in the Marketing Cloud journey VIP Customer Cart Recovery with the new cart price.
10. **Logging and attribution:** John redeems the offer, which creates a log attribution and conversion metrics.
11. **Feedback analysis:** The outcome is analyzed to further determine offers, time to recovery, and other optimization factors.

A sales representative, David, is engaged in a discovery call with a new prospect. An intelligent agent actively monitors the call in real time, providing immediate support to David by answering the prospect's questions.

**Example:** If the prospect inquires about a specific product specification, the agent automatically retrieves the relevant details and delivers them to David via Slack or a private message.

- **Trigger:** A prospect asks a question requiring specific product information during a discovery call with a sales representative (David).
- **Agent Action:** The ambient agent continuously analyzes call logs and messages, intelligently identifying and fetching required information.
- **Process:**
	1. The agent parses the call transcript in real time.
		2. It automatically identifies key action items and retrieves relevant information.
		3. In this instance, the agent fetches product information directly from Salesforce.
		4. It then automatically presents the retrieved information to David via Slack or a private message.

**Recipe**

There are prerequisites in this recipe that require real time speech-to-text capabilities, and we assume they are available through your communication provider. For example, here is a recipe to integrate Zoom calls.

**Prerequisite:** Example real-time transcription of a Zoom call:

- Create a Zoom app in the Zoom Developer Platform with required scopes for reading recording, webhook send, and meeting stream. Enable required product features such as Realtime Media Streams (RTMS).
- Set up an intermediate signaling server ([Zoom RTMS sample](https://github.com/zoom/rtms-samples/tree/main/audio/send_audio_to_aws_transcribe_service_sdk)) that receives the audio stream, forwards it to the Amazon Transcribe service, and gets back the transcribed text. The transcripts are then published to Salesforce as a platform event.

**Design Time**

1. Set up a Sales Call Realtime Response agent.
	| Create agent from template | → | Add Assist Call topic | → | Add topic instructions | → | Create transcript analysis action |
	| --- | --- | --- | --- | --- | --- | --- |
	|  |  |  |  |  |  | ↓ |
	|  |  | Add actions to topic | ← | Create Slack insights action | ← | Create product spec action |
	1. Create an agent from the [Agentforce Employee Agent template](https://help.salesforce.com/s/articleView?id=ai.agent_employee_agent_setup.htm&type=5).
		2. Add a new topic, Assist Call, with the description that this agent listens to live transcripts, understands the intent, and helps with product data.
		3. Add topic instructions to parse transcripts, retrieve product specifications, and send Slack messages.
		4. Create actions.
		- Analyze Call Transcript action: Analyzes the call transcript data received in real time and extracts key questions or actions
				- Get Product Spec action: Queries product knowledge articles
				- Send Slack insights to the "internal" user
		5. Add the actions to the topic.
2. Set up a Product Knowledge data library.
	| Create new data library | → | Add knowledge articles | → | System chunks and indexes | → | Ground library in action |
	| --- | --- | --- | --- | --- | --- | --- |
	1. [Create a new data library](https://help.salesforce.com/s/articleView?id=ai.data_library_setup.htm&type=5) from Setup. Name it "Product Knowledge."
		2. Add the knowledge articles that contain the product information.
		3. Behind the scenes, the documents are automatically chunked, indexed, and made ready to use.
		4. Use the grounding in the Get Product Spec action.
3. Publish the real-time transcript to Salesforce via Pub/Sub API.
	| Server receives audio transcript | → | Server publishes platform event |
	| --- | --- | --- |
	1. Create a platform event, Transcript\_Segment\_\_e, with the fields Call Id, Sequence, Speakers, Segment Start Time, Segment End Time, Duration, and Transcript Data.
		2. In your signaling server (see the prerequisite section), once you receive the transcribed text from audio, immediately publish the data via the Transcript\_Segment\_\_e event. You can publish the event to Salesforce using [any of these methods](https://developer.salesforce.com/docs/atlas.en-us.platform_events.meta/platform_events/platform_events_publish.htm): Flows, Apex, Salesforce APIs, or Pub/Sub API.
4. Wire Flow to subscribe to the published Transcript\_Segment\_\_e event.
	| Create event-triggered flow | → | Subscribe to Transcript event | → | Add agent invocable action | → | Send payload to agent |
	| --- | --- | --- | --- | --- | --- | --- |
	|  |  |  |  |  |  | ↓ |
	|  |  |  |  |  |  | Agent sends Slack DM |
	1. Create a new platform-event-triggered flow, Discovery Call Insights.
		2. Select the Transcript\_Segment\_\_e event that the flow should subscribe to.
		3. [Set up a custom agent](https://help.salesforce.com/s/articleView?id=ai.agent_custom_invocable_action_flow_set_up.htm&type=5) invocable action in Flow Builder, and select the Sales Call Realtime Response agent. Send the event payload to route to the Assist Call topic. After the question is derived from the topic, the question is sent to the Get Product Spec action for an answer.
		4. The final answer is compiled and sent immediately to the user via a Slack DM.

**Agent Runtime Process Flow**

Once the agent is set up and deployed, the following sequence of steps occurs at runtime.

| User starts Zoom call | → | Server transcribes and publishes | → | Flow invokes Response agent | → | Agent queries knowledge base |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  | ↓ |
| Analytics refine agent performance | ← | Agent compiles call summary | ← | Agent continues listening | ← | Agent sends Slack DM |

1. **Call initiation:** David starts a discovery call with a prospect in a Zoom call. Zoom RTMS streams the live audio to the signaling server transcription endpoint.
2. **Real-time transcription:** The signaling server receives the audio, transcribes the audio to text, and publishes a Transcript Segment platform event in Salesforce Platform.
3. **Agent listening and context classification:** Salesforce receives the platform event and triggers the Discovery Call Insights Flow.
4. The flow initiates the Sales Call Realtime Response agent that receives the segment, identifies questions (such as "Does the Toaster 2XP integrate with mobile devices?"), and classifies them under the Assist Call topic.
5. **Knowledge retrieval:** The agent triggers the Get Product Spec action and queries the knowledge data for matching answers.
6. **Send private Slack DM:** The agent executes Send Slack Insight, posting to David's Slack DM: "Product *Toaster 2XP* can be integrated with Apple and Android devices and can connect via Bluetooth. Once the app is installed, simply connect via Bluetooth and operate the toaster. Here is the link to the manual."
7. **Real-time continuation:** The agent continues receiving transcript text; if multiple insights emerge, it threads contextual Slack replies without disrupting the call flow.
8. **Post-call summary:** At the end of the session, the agent automatically compiles a summary: key questions, actions taken, and referenced products.
9. **Continuous improvement:** Agentforce Analytics evaluates transcript–response latency, product match accuracy, and sales outcomes to refine topic instructions over time.

A sales manager, Bob, tasks an autonomous agent with a goal: "Increase our sales pipeline in the California manufacturing sector by $5M in the next 60 days."

- **Trigger:** The manager assigns the goal through a command in Slack.
- **Agent Action:** The autonomous agent begins its planning and execution loop.
- **Process:**
	1. **Research:** The agent queries Salesforce Data 360 and external data sources (via MuleSoft) to identify companies in California's manufacturing sector that are not current customers.
		2. **Qualify:** It analyzes these companies, looking for buying signals like recent funding rounds, new executive hires, or relevant job postings. It scores and prioritizes the top 20 prospects.
		3. **Identify Contacts:** It finds key contacts (such as VPs of operations and plant managers) at these companies.
		4. **Outreach:** It drafts personalized outreach emails for each contact, referencing specific company news or pain points. It schedules these emails to be sent over the next week.
		5. **Follow-up:** It tracks email opens and replies. A positive reply from a prospect triggers an analysis of their calendar to suggest meeting times, automatically generating a Salesforce event and a new Opportunity upon confirmation.
		6. **Report:** It provides weekly progress reports to the sales manager in Slack.

**Recipe**

This is a multi-agent scenario where each agent performs a specific task and hands the context, data, and control off to the next agent. We will use a few custom headless agents for research and qualification, and the out-of-the-box Sales Development Rep (SDR) agent for prospect outreach and monitoring. We will also assume that Bob's company uses ZoomInfo for its market research. The company also receives supplier network data that is persisted in a database and contains valuable information about the companies they partner with.

**Design Time**

1. Set up multi-agent architecture.
	| Research agent gathers intelligence | → | Qualification agent scores lead | → | SDR agent begins outreach |
	| --- | --- | --- | --- | --- |
	1. Research agent: Queries Data 360 and external sources via MuleSoft
		2. Qualification agent: Prioritizes, scores, and enriches leads
		3. SDR agent: Gets lead assignments, executes outreach, follows up, and schedules meetings. Monitor SDR agent activity and progress with Agentforce Analytics for SDR agent.
2. Discover and ingest new company data.
	| Create new Data Space | → | Ingest Salesforce CRM data | → | Ingest ZoomInfo data | → | Ingest supplier database data |
	| --- | --- | --- | --- | --- | --- | --- |
	1. Setup a new Data Space called Sales and Marketing. This new data space will hold all the data needed for autonomous agents.
		2. Use Salesforce connectors to flow the Lead, Account, Contact, and Opportunity CRM data into the data space.
		3. Configure a Data 360 connector for ZoomInfo. Flow the data into the Data 360 Sales and Marketing Data Space.
		4. Configure the Anypoint Salesforce Data 360 connector to connect to the supplier database and ingest the data into Data 360.
3. Set up a platform event to initiate the headless Research and Qualification agent. Create new platform event
	1. Create a new AgentGoal\_\_e platform event with the field goal that captures the human user's high-level goal.
4. Set up a Goal Orchestrator agent, a conversational AI agent that receives the user's goal and orchestrates it to other agents.
	| Create agent from template | → | Add Parse Goal topic | → | Add topic instructions | → | Create Goal Event action |
	| --- | --- | --- | --- | --- | --- | --- |
	|  |  |  |  |  |  | ↓ |
	|  |  |  |  |  |  | Add action to topic |
	1. Create an agent from the [Agentforce Employee Agent template](https://help.salesforce.com/s/articleView?id=ai.agent_employee_agent_setup.htm&type=5).
		2. Add a new topic, Parse Goal, with the description that this agent understands the goal intent and is able to call additional agents as needed.
		- Add topic instructions to parse the goal and trigger events to other agents.
		3. Create a Goal event, AgentGoal\_\_e.
5. Set up a Lead Research and Qualification agent, which is triggered by an orchestrating agent.
	| Create Research topic | → | Create deduplication action | → | Create lead enrichment action | → | Create lead scoring action |
	| --- | --- | --- | --- | --- | --- | --- |
	|  |  |  |  |  |  | ↓ |
	|  |  |  |  | Add actions to topic | ← | Create lead qualification action |
	1. Create a Prospect Research topic with the description "Research new leads in a region or state."
		2. Create actions.
		- Deduplicate Lead Apex action: Check and validate new leads against existing customers
				- Enrich Lead Apex action, which uses a prompt template: Looks into the unstructured marketing insight and supplier database data to enrich lead data
				- Score Lead action: Proactively score a lead with updated lead data
				- Qualify Lead for Agent action: Based on the scoring, assign parameters that qualify the lead for an SDR agent
6. Set up an Agentforce SDR agent to perform outreach, lead nurturing, and meeting scheduling.
	| Create SDR agent from template | → | Configure agent knowledge base | → | Configure agent email settings | → | Set lead assignment rules |
	| --- | --- | --- | --- | --- | --- | --- |
	|  |  |  |  |  |  | ↓ |
	|  |  |  |  |  |  | Define qualifying lead criteria |
	1. Create a new SDR agent from the Setup page using the preconfigured [Lead Nurture Agent template](https://help.salesforce.com/s/articleView?id=sales.sales_agent_sdr_setup_agent_builder.htm&type=5). Configure the email settings and lead assignment rules, selecting the Lead object or Contact object and defining the qualifying criteria (threshold lead score and new lead) for assignment rules.
		2. [Set up Agentforce Lead Nurturing](https://help.salesforce.com/s/articleView?id=sales.einstein_sdr_setup.htm&type=5) by configuring the agent, assigning permissions, and setting up the cadence and assignment rules.
		3. [Configure necessary knowledge](https://help.salesforce.com/s/articleView?id=sales.sales_agent_sdr_setup_data_cloud.htm&language=en_US&type=5) for the SDR agent to answer questions.
7. Set up a new flow to subscribe to the published AgentGoal\_\_e event.
	| Create event-triggered flow | → | Subscribe to Agent Goal event | → | Add agent invocable action |
	| --- | --- | --- | --- | --- |
	1. Create a new platform-event-triggered flow called Route Goals to Agents.
		2. Select the Agent Goal event that the flow should subscribe to.
		3. [Set up a custom agent](https://help.salesforce.com/s/articleView?id=ai.agent_custom_invocable_action_flow_set_up.htm&type=5) invocable action in Flow Builder, and select the Lead Research and Qualification agent.

**Agent Runtime Process Flow**

Once the agent is set up and deployed, the following sequence of steps occurs at runtime.

| User assigns high-level goal | → | Orchestrator agent creates event | → | Flow routes goal to agent | → | Research agent qualifies lead |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  | ↓ |
|  |  | Monitor agent with analytics | ← | SDR agent schedules meeting | ← | SDR agent begins outreach |

- **Goal assignment:** Bob tasks an autonomous agent to "increase pipeline in California manufacturing by $5M in 60 days."
- **Goal orchestration:** The autonomous Goal Orchestrator agent receives the goal, parses the intent, and creates a platform event, AgentGoal\_\_e. The Goal Orchestrator agent is designed to continuously expand its capabilities to handle multiple goals. You can expand it to add additional orchestration capabilities or ask the user for clarification to better understand the intent and initiate the goal.
- **Routing:** The Flow Route Goals to Agents gets triggered and calls the Lead Research and Qualification agent.
- **Research:** The Lead Research and Qualification agent queries Data 360 for new lead information, deduplicates against existing customers, pulls additional market research data from Data 360, and enriches the lead. It further scores the lead, identifies key contacts, and qualifies the lead.
- **Outreach:** Once the lead is qualified, the lead becomes eligible for the SDR agent via the lead assignment rules. The SDR agent does the initial outreach and maintains conversations with the contact by answering questions related to the product.
- **Follow-up:** At the end of the cadence or at the request of the lead, the agent prompts for a meeting schedule if the lead is qualified for service rep engagement. It then schedules the meeting and exits the flow.
- **Agent Analytics:** The [SDR Agent Analytics](https://help.salesforce.com/s/articleView?id=sales.sales_agent_sdr_analytics.htm&type=5) dashboard provides insights into how effectively the agent performs.

A long-time customer is experiencing a multifaceted issue: they were overbilled, the replacement part they received was incorrect, and their service is now disconnected.

- **Trigger:** The customer initiates a chat, and the initial conversational agent quickly recognizes the complexity and escalates to an agent swarm.
- **Agent Action:** An orchestrator agent takes charge.
- **Process:**
	1. **Orchestrator:** Maintains the conversation with the customer, providing updates
		2. **Orchestrator delegates:** Using the A2A protocol implementation, the Orchestrator discovers "related agents" (Billing, Logistics, and Provisioning) with the required capabilities and dispatches tasks.
		- To **Billing Agent:** "Investigate invoice #INV-7890 for customer X. Are there discrepancies?"
				- To **Logistics Agent:** "Check tracking number #TN-12345 for customer X. Confirm the part number shipped and the current inventory for the correct part."
				- To **Provisioning Agent:** "Check service status for account #ACC-5678. If disconnected, what is the reason code?"
		3. **Specialized agents execute:** Each agent receives the A2A request, queries its respective system, and formulates a response.
		4. **Synthesis:** The agents report their findings back to the Orchestrator via A2A responses. The Orchestrator synthesizes the information: "The customer was indeed overbilled by $50. The wrong part was shipped due to a warehouse error. The service was disconnected automatically due to the billing issue."
		5. **Acknowledgement:** The Orchestrator informs the customer about the issue and offers to escalate the issue to a human service rep with clear guidance on the next steps.
		6. **Resolution:** It then proposes a complete solution to the service rep for approval. The service rep joins the conversation. The service rep quickly looks at all the data relevant to the issue, including the agent's recommended solution: "Create a new shipping order for the right part with expedited shipping. Initiate a return for the wrong part. Approve 10% discount on the new order and upsell the part with the latest improved version. Update payment information and offer to set up a recurring billing arrangement."

**Recipe**

This recipe outlines the implementation of a collaborative agent system designed to tackle complex customer service issues involving multiple facets. By using an orchestrator agent to delegate tasks to specialized agents (Billing, Logistics, and Provisioning) via an A2A protocol and then synthesizing their findings, the system provides comprehensive solutions and seamlessly integrates service reps for final approval and customer interaction.

**Design Time**

1. [Set up Enhanced Chat](https://help.salesforce.com/s/articleView?id=service.miaw_setup_stages.htm&type=5) as the customer's chat entry point so they can open the Agentforce window in the web page.
2. Set up an Agentforce Billing Agent, a headless specialized agent that can take an order or invoice and perform a billing inquiry.
	| Create agent from template | → | Define Billing Inquiry Topic | → | Create custom flow action | → | Add action to topic |
	| --- | --- | --- | --- | --- | --- | --- |
	1. Enable Agentforce and create an Employee Agent from the [Agentforce Employee Agent template](https://help.salesforce.com/s/articleView?id=ai.agent_employee_agent_setup.htm&type=5).
		2. Define a topic, Billing Inquiry, with the description "Investigate invoice discrepancies, payment issues, and billing errors."
		1. Add a custom flow action, Check Invoice Discrepancy, with an input of Invoice Number, Customer ID, and Date Range, and an output of Discrepancy Amount, Root Cause, and Affected Transactions.
3. Set up an Agentforce Logistics Agent, a headless specialized agent that can verify shipments, track shipping, and check inventory.
	| Create agent from template | → | Define Shipping Verification topic | → | Create custom flow action | → | Add action to topic |
	| --- | --- | --- | --- | --- | --- | --- |
	1. Enable Agentforce and create an Employee Agent from the [Agentforce Employee Agent template](https://help.salesforce.com/s/articleView?id=ai.agent_employee_agent_setup.htm&type=5).
		2. Define a topic: Shipping Verification, with a description to verify shipping for invoice.
		1. Add a custom Flow action, Verify Shipping Details, with an input of Invoice Number, Customer ID, and Date Range, and an output of Shipped Part, Date, and Inventory Status.
4. Set up an Agentforce Provisioning Agent, a headless specialized agent that can verify provisioning and service status.
	| Create agent from template | → | Define Service Check topic | → | Create custom Flow action | → | Add action to topic |
	| --- | --- | --- | --- | --- | --- | --- |
	1. Enable Agentforce and create an Employee Agent from the [Agentforce Employee Agent template](https://help.salesforce.com/s/articleView?id=ai.agent_employee_agent_setup.htm&type=5).
		2. Define a topic, Service Check, with a description to verify service connectivity and account status.
		1. Add a custom Flow action, Verify Service, with an input of Customer Id and Asset Id, and an output of Service Status and Service Exception Reason.
5. Expose Billing, Logistics, and Provisioning agents as A2A servers and register them in Agent Registry.
	| Expose agents via MuleSoft | → | Register agents in registry |  |
	| --- | --- | --- | --- |
	1. In the absence of direct A2A support on Agentforce Agents, MuleSoft connectors can be used to [expose agent APIs as A2A servers](https://www.mulesoft.com/platform/ai/a2a-support).
		2. Register these A2A servers in [Agent Registry](https://www.mulesoft.com/platform/exchange).
		3. Use Anypoint Agent Fabric for orchestration of agents.
		1. [MuleSoft Agent Broker](https://www.mulesoft.com/ai/agent-broker) can help in orchestrating any agent across platforms based on agent capabilities mentioned in the agent cards.
6. Set up an Agentforce Help Agent, conversational AI agent that interacts with customers, assesses complexity, and coordinates with multiple specialized agents to resolve the issue.
	| Create Service Agent | → | Define Investigation topic | → | Create notification action | → | Define Orchestration topic |
	| --- | --- | --- | --- | --- | --- | --- |
	|  |  |  |  |  |  | ↓ |
	| Define Escalation topic | ← | Create Create Case action | ← | Create Call Agent action | ← | Create agent orchestration flow |
	| ↓ |  |  |  |  |  |  |
	| Create Omni-Channel flow | → | Connect flow for escalation |  |  |  |  |
	1. Enable Agentforce and [create a Service Agent](https://help.salesforce.com/s/articleView?id=ai.service_agent_setup.htm&language=en_US&type=5) in Agentforce Builder to handle conversations and trigger custom actions.
		2. Define a topic, Service Investigation, with a description and instructions so that the agent naturally recognizes a complex [topic](https://help.salesforce.com/s/articleView?id=ai.copilot_topics.htm&type=5) with, typically, multiple simultaneous issues.
		1. [Create custom agent actions](https://help.salesforce.com/s/articleView?id=ai.copilot_actions_custom.htm&type=5).
			- Status Notification action to acknowledge the issue and provide progress updates
		3. Define an Orchestration topic that can call other agents via actions.
		1. Create a Call Agent action that calls a Flow action. The Flow action has several agent actions and can initiate each of the headless agents: the Billing Agent, the Logistics Agent, and the Provisioning Agent.
				2. Create a Create Case action that creates a case, adds details, and sets the status.
		4. Define an Escalation topic with a description to escalate to a service rep.
		5. Create and activate an outbound Omni-Channel flow.
		- Add it to the Connections tab in the Agent for escalation with an escalation message.

**Agents Orchestration Process Flow**

Anypoint Code Builder now supports building agent brokers. An agent broker is an intelligent routing and orchestration layer that connects agents across domains and engages the best-fit agents and tools. MuleSoft Dev Agent generates the code to set up a foundation for the broker.

Based on agent capabilities mentioned in the agent cards (A2A servers), which were previously registered with Agent Registry, further configurations are done automatically by Anypoint Code Builder. Lastly, we can deploy this agent broker to the cloud.

Once the agent broker is available for consumption, these requests are routed to the proper agents. A broker receives a prompt and uses the LLM to decompose it into tasks and determine which agent to call first. In each iterative loop, it determines if it has successfully addressed the original prompt or if it needs to work with additional agents to complete the job.

| Agentforce Help Agent | → | Mulesoft Agent Broker | → | Billing Agent as A2A server | → | Logistics Agent as A2A server |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  | ↓ |
|  |  | Help Agent gets response | ← | Broker aggregates response | ← | Procurement Agent as A2A server |

**Agent Runtime Process Flow**

Once the agent is set up and deployed, the following sequence of steps occurs at runtime.

| Customer starts chat | → | Customer states multiple issues | → | Agent investigates order details | → | Orchestrator calls specialist agents |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  | ↓ |
| Orchestrator synthesizes resolution plan | ← | Provisioning Agent finds issue | ← | Logistics Agent confirms error | ← | Billing Agent finds discrepancy |
| ↓ |  |  |  |  |  |  |
| Agent escalates to service rep | → | Service rep offers resolution | → | System agent executes tasks | → | Agent updates and closes case |

1. **Chat launch:** A customer opens the Agentforce chat (embedded service). Session and Contact context load after the customer is logged in.
2. **Greeting and intent:** The agent greets the customer. The customer, with clear frustration, notifies about overcharges, the wrong part, and disconnected service.
3. **CRM lookup:** The agent triggers the Get Latest Order action and queries Salesforce (order summary/orders) for the customer's most recent record. The agent then confirms the order in context and notifies the customer that it will investigate. It further looks up the invoice ID, the tracking number associated with the invoice, and the asset ID related to the service.
4. **Orchestrator activation:** The orchestrator agent receives the escalation and order ID and then creates a case. It passes the context data to and communicates with three agents: the Billing Agent, the Logistics Agent, and the Provisioning Agent.
5. **Billing Agent response:** The Billing Agent returns with details on the part, unit cost, and the total cost. It also notes a discrepancy between the part in the order and the part in the invoice. The Billing Agent looks up the price for the part in the order and reasons for the overcharge.
6. **Logistics Agent response:** The Logistics Agent returns with details on the shipped part and the exception notes created by the logistics system that state the wrong part could have been sent due to tagging issues. The Logistics Agent also verifies that the issue is now fixed and the correct part is available in original and newer versions.
7. **Provisioning Agent response:** The Provisioning Agent returns with details on the service disconnect and the issue about the expired payment information. It also provides the notifications sent to advise the customer to update the payment information.
8. **Orchestrator synthesis:** The orchestrator agent synthesizes the responses from all these agents and composes a solution by looking at knowledge articles for each of the issues. First, it looks up information on the wrong part and initiates a return. Second, it offers a discount for the issue based on the resolution policy documents and also recommends an upgrade to a newer version that the customer can buy (but there is a price difference). Third, it needs new payment information from the customer, so it escalates to the service repo to communicate the resolution.
9. **Escalation:** The orchestrator agent escalates to the service rep—providing all the necessary context, investigation notes, and resolution recommendations along with necessary approvals—and brings the service rep into the call.
10. **Human in the loop:** The service rep thanks the customer for their patience, apologizes for the trouble, and explains the issue. The service rep then offers a 10% discount for the part as compensation and also informs the customer of a new upgraded part and its benefits. Lastly, they explain about the disconnect, get the new payment information, and update the system.
11. **Proactive restoration:** The AI agent watches the conversation and proactively acts on restoring the service, ordering the upgraded part, and creating a new invoice with the discount and adjusted price.
12. **Case closure:** Finally, it compiles the summary, updates the case, and closes the case.

For an agent to be effective, it must be able to integrate with a broad set of enterprise data and tools. This provides the essential context an agent needs to perform its configured goal. The Agentforce framework provides a sophisticated integration architecture that integrates data that is both **internal** to Salesforce and **external** to Salesforce.

This section explores the patterns for connecting agents to these resources. These patterns are built upon two foundational approaches for integration.

- **Internal integration (data access and tool access):** For resources within the Salesforce ecosystem, an agent has two ways to operate.
	- **Data access:** The Agentforce core runtime is deeply integrated with Data 360, allowing it to *directly* query internal data services. It can natively formulate and execute queries against **Data Graphs** to get a 360-degree view of the customer, perform semantic searches via **RAG** to understand unstructured knowledge, and access bulk information using the **Data 360 Query API.** This direct path is optimized for speed and flexibility in data retrieval.
		- **Tool access:** When a task involves complex business logic or multi-step processes, or when it requires strict governance, its capabilities are encapsulated in **Actions**. Built with Apex or Flow, these actions provide a secure and reusable interface for the agent to do more than just read data—they allow it to update records, trigger platform events, or execute any established business process.
- **External integration (MCP/A2A):** When an agent needs information outside of Salesforce (for example, from an external application, a microservice, or another agent), it uses the **Model Context Protocol (MCP).** This open standard provides a common language for interoperability. MCP Servers can be added from [AgentExchange](https://agentexchange.salesforce.com/) or an admin can add in Agent Registry or an Apex callout to the MCP server. Then the action initiates the request to an external MCP server, bridging the internal and external worlds in a structured way. Similarly, when an agent needs to communicate with another agent, the **Agent2Agent (A2A)** protocol facilitates this interaction. This allows for the creation of complex, multi-agent systems where specialized agents can collaborate to solve intricate problems, promoting modularity and reusability.

The following patterns are organized around the specific data integration themes agents need. We will demonstrate how these patterns are applied to solve distinct data challenges, from **connecting to external applications** using MCP to accessing **high-volume bulk data** in Data 360, real-time **transactional records**, and **unstructured content** using the powerful combination of direct access and formal actions within Data 360.

**Problem**

An agent's effectiveness depends on its ability to operate external tools. However, these tools—from legacy ERPs to modern SaaS applications—lack a shared language. Each has a unique API, authentication model, and data format. This forces developers into a brittle and unscalable cycle of building and maintaining custom, point-to-point integrations for every new tool the agent needs to use.

**Context**

Consider an agent tasked with resolving a damaged shipment case. To succeed, it must interact with three different external systems: it needs to query a **supplier's API** to check for replacement inventory, call a **logistics partner's service** to arrange a new delivery, and access a **financial system** to process a credit. Without a common protocol, the agent would require three separate, bespoke integrations, each a potential point of failure. [MCP](#2-agent-interoperability-a2a-and-mcp) provides a standardized communication layer to make these interactions seamless and reliable.

Following are recipes for how you integrate external services exposed via MCP to your agent.

![Recipes to Integrate MCP Tools](https://a.sfdcstatic.com/developer-website/prod/images/architect/agent-taxonomy-ambient-agents.png)

**Recipe 1:** **Enabling External Tools with MCP**

**Problem**

Organizations run on a mix of legacy ERPs and modern SaaS, but integrating them with an agent is hard because there's no common protocol—each tool has its own APIs, authentication, and data model. Developers end up building and maintaining custom point-to-point connectors for every tool, producing fragile, unscalable, and costly integrations.

**Pattern**

The agent invokes an external tool (exposed via MCP) through a structured action, allowing it to use specialized tools beyond the Salesforce platform.

**Context**

- The agent acts as a proxy for a set of tools that exist outside the Salesforce platform.
- These external tools may have diverse APIs, authentication mechanisms, and data formats.
- A standardized communication protocol is required to enable seamless interaction between the agent and these external tools.
- Reusability is a key concern, as the same external tools may be utilized by multiple agents for different purposes.

**Interactions**

1. **Trigger:** A user request or an internal event within Agentforce necessitates the use of an external tool.
2. **Intent to act:** The Agentforce Agent identifies the intent and determines that an external MCP-based tool is required.
3. **Planner (internal):** The Agentforce Agent's planner selects the appropriate MCP tool or action based on its configured instructions and available tools.
4. **Execution:** The Agentforce Agent sends an MCP-compliant request to the external MCP server (for example, via an Apex callout to a MuleSoft endpoint, which then routes to the external MCP server).
5. **External processing:** The external MCP server processes the request, interacts with the underlying external application, and prepares an MCP-compliant response.
6. **Result**: The external MCP server returns the response to the Agentforce Agent.
7. **Follow-up:** The Agentforce Agent processes the response, updates its internal state, and continues its task or provides feedback to the user.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Flexibility | Access to diverse external capabilities | Initial development for MCP server/integration layer |
| Modularity | Agent capabilities are decoupled from external tools | Requires careful API design and versioning |
| Scalability | Uses external system's scalability | External system's performance becomes a dependency |
| Standardization | Standardized protocol (MCP) | Adoption and/or wrapper |
| Security | Centralized security for external access | Management of credentials and access policies for external systems |
| Maintainability | Updates to external tools do not require agent changes. MCP can signal changes | Cost of frequent changes |

An agent's decision-making logic is only as sound as its underlying data. For an agent to act intelligently, it must have a rich, real-time understanding of the world around it. Without a defined data ingestion architecture, the agent cannot access or process the high-volume, real-time information that is essential for it to function.

**Integrate Transactional Data with Agents**

**Problem**

Agents frequently need to perform low-latency read/write operations on individual records residing in systems of record (for example, updating a case or fetching an order status). These actions require data integrity and reliability to ensure consistency of the underlying data model. The core architectural challenge is providing a secure, real-time, and scalable pattern for this transactional data access without creating brittle point-to-point integrations.

**Context**

Successfully connecting an agent to these records requires a robust architecture composed of several **core components.**

- **Transactional systems:** These are the authoritative sources of the data, such as systems of record, like **Salesforce**, **Workday** or **SAP,** or services hosted on platforms like **AWS.**
- **Integration layer:** A powerful integration layer, typically handled by **MuleSoft,** is crucial for securely connecting to these disparate systems, transforming data, and exposing it to the Agentforce platform.
- **MCP servers:** To ensure interoperability, agents communicate with these external systems using the MCP standard. The integration layer may connect to various **MuleSoft, Heroku, or third-party MCP servers** that host the external services or agents.
- **Agent Exchange:** This component acts as a directory or switchboard, allowing the Salesforce agent to discover and securely connect to the correct external service or agent to complete its task.

**Recipe 1: Direct Record Operations via MCP**

**Pattern**

The agent uses MCP to connect to a transactional data system and performs stateful CRUD operations on specific, identified records with immediate consistency requirements.

**Context**

- Conversational, collaborative agents must transact system-of-record data in the flow of work.
- The system of record is an external system.
- Transactions need to be idempotent.

**Key Components**

- **Agentforce Agent:** With topics and instructions to make a transactional update. Actions calls an external MCP server or Agentforce Exchange–registered MCP server.
- **MCP server:** The MCP server that exposes the transaction data and function (for example, tool=billing.update\_record with input data)
- **External system of record:** The system where the stateful change occurs

**Interactions**

1. **Trigger:** A command or event occurs requiring a transaction on a record.
2. **Intent to act:** An Agentforce Agent identifies a state change intent.
3. **Planner (internal):** The planner chooses an MCP tool.
4. **Execute:** The tool is executed after policy-, record-, and field-level access checks pass.
5. **Result:** The MCP server returns a response
6. **Follow-up:** The Agentforce Agent processes the response.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Speed | One tool call | More governance overhead |
| Idempotency and Safety | Safe retries | Implementation to support dedupe and idempotency |
| Scalability | Can scale easily | Connection overhead |
| Consistency | Clear and explicit | Atomic |
| Safety | Guardrails and policies can be implemented. | Operation overhead to cascade policy changes |
| Observability | Correlation and audit are available for operation. | Increased telemetry costs |

**Recipe 2: Complex Orchestration via Mulesoft API**

**Pattern**

The agent leverages Mulesoft API for complex, multi-step, cross-system atomic transactions. This provides a single, governed endpoint, ensuring reliable end-to-end processing and avoiding the consistency, reliability, latency, and data issues associated with direct calls to individual systems.

**Context**

- Conversational and autonomous agents often need to perform several operations reliably.
- There are multiple transactional systems and operations in a transaction.
- Workflows require transaction/rollback, retries, and policy enforcement.
- Transaction needs are real-time, idempotent, observable, and compliant.

**Interactions**

1. **Trigger:** A command or event occurs, requiring a complex transaction to be completed.
2. **Intent to act:** The Agentforce Agent identifies the intent.
3. **Planner (internal):** The planner chooses an [invocable action for API or API action](https://help.salesforce.com/s/articleView?id=platform.api_catalog_activate_agent_topics_and_agent_actions.htm&type=5).
4. **Execution:** The API is executed and a response returned.
5. **Follow-up:** The Agentforce Agent processes the response.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Speed | One call for multiple distributed operations | Development and operational overhead |
| Idempotency and Safety | Safe retries/SAGA support | Complexity |
| Scalability | Can scale easily, can be async | Eventual consistency for Async |
| Safety | Policies in API layer | Operation overhead to cascade policy changes |
| Observability | Correlation and audit available for tracing | Increased telemetry costs |

**Integrate Analytical Data with Agents**

**Problem**

Organizations have invested heavily in analytical infrastructure—data warehouses and lakes, real-time analytical systems, and business intelligence platforms—yet AI agents remain disconnected from these systems. This creates a gap in an agent's ability to get an enriched context (for example, that a customer had returned parts three times in the last quarter) to help make better decisions (in this case, escalation).

**Context**

An agent's operational intelligence is derived from its ability to synthesize information from fundamentally different data formats and sources. This architectural pattern, therefore, is not designed for a single use case but as a foundational data ingestion framework. An effective agent must be equipped to process structured sources to perform logical, data-driven analysis; an agent requires access to high-volume, structured feeds. This includes integrating with enterprise **data lakes** (via zero copy integration with Data 360), processing **middleware-transformed** data streams, or ingesting batch files such as **CSVs**.

**Recipe 1: Data Lakes Integrated via Data 360 Zero-Copy**

**Problem**

Organizations face high costs when using traditional data pipelines to copy, manage, and transform analytical data stored in data lakes (for example, Snowflake). Historically, analytics have been largely offline, resulting in missed opportunities for timely action.

**Pattern**

The agent queries zero copy data (and calculated insights) available in Data 360 rather than querying external data warehouses for critical insights. This helps agents ground both transactional and analytical data for better decision-making.

**Context**

- Your organization stores customer and operational data in data warehouses and lakes.
- Your agents need access to aggregated metrics, historic trends, and analytical insights.
- Your agent's context needs both transactional and analytical data (consider a research agent's need for historical trend data).

**Interactions**

1. **Trigger:** An agent receives a query regarding an insight that requires access to analytical data or a calculated insight.
2. **Execution:** The agent executes an action that calls Data 360 Calculated Insights via Query API, and the calculated insight is returned.
3. **Follow-up:** The Agentforce Agent processes the response.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Data Movement | None; zero copy | Compute cost |
| Latency | From days or weeks to near-real-time | SLAs |
| Scalability | Unlimited data volume | Compute cost |

**Recipe 2: Triggering Actions from Data Streams**

**Problem**

Organizations continuously generate valuable information from business activities like web site visits, calls, meetings, chats, and sensor data. However, by the time these interactions become available or retrieved from data warehouses, critical insights are lost, and the opportunity for timely intervention has passed. Consequently, organizations miss the majority of actionable intelligence needed in real-time, which is often buried in these ephemeral streams. This leads to gaps, missed coaching opportunities, and decisions made without complete context.

**Pattern**

The agent receives real-time or near-real-time insights from [streaming insight](https://help.salesforce.com/s/articleView?id=data.c360_a_create_streaming_insight.htm&language=en_US&type=5) or a [real-time insight](https://help.salesforce.com/s/articleView?id=data.c360_a_create_real_time_insight.htm&language=en_US&type=5) in Data 360 via a data action, or the agent accesses a streaming insight in real time by querying an MCP server that interfaces with a real-time processing engine like Apache Flink.

**Context**

- Streaming systems such as platform events, Pub/Sub API, and RTEM generate enormous amounts of stream data.
- Stream processing systems like Data 360 and Apache Flink process these individual events as they arrive.
- Agentforce needs to query the stream systems (for example, the most recent 30-second transcript for the live meeting with additional context) or gets triggered by data action (for example, fraud detection).
- There's a need for near-real-time, low-latency action.

**Interactions**

1. **Stream emit:** The source system emits a continuous stream of data.
2. **Stream processing:** Stream processing engines like Data 360 or Apache Flink processes the information.
3. **Transform:** Insights are aggregated, transformed, and synthesized into agent-aware data in middleware (for complex transformation) or in Data 360.
4. **Stream insight event:** A Data 360 Data Action is triggered for synthesized data (for example, a transcript of a 30-second audio stream).
5. **Enrich:** An agent adds context and detects intent.
6. **Execute:** The agent executes action.
7. **Follow-up:** The agent waits for the next streaming insight.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Latency | Available in seconds | Compute and implementation cost |
| Coupling | Producers are independent of consumers. | Harder to debug and trace |
| Scalability | Can scale | Limits |
| Ordering | Incremental context build | Out-of-order arrival |
| Value | Near-real-time insight | Governance and compliance overhead |

**Integrate Semantic Data with Agents**

Organizations have business artifacts—catalogs, manuals, policies, knowledge graphs, relationship maps—in different formats and shapes. To move beyond simple task execution and engage in sophisticated reasoning, agents must be able to comprehend this data where most human knowledge is stored.

**Recipe 1: RAG: Unlocking the Power of Unstructured Data for Agents**

**Problem**

Organizations frequently possess unsearchable information that hinders agents' ability to access it with confidence. This deficiency often leads to incomplete responses from agents, lacking the necessary contextual depth and verifiable citations to establish trust. Consequently, there is a clear need for a standardized method to enable agents to consistently retrieve semantically relevant and accurate content.

**Pattern**

This pattern provides the architecture for enabling agents to ingest and interpret a wide variety of unstructured information, from internal documents to public web content. Giving an agent access to this data is the key to unlocking advanced capabilities like market sentiment analysis, document summarization, and competitor research.

**Context**

- Knowledge is in files in different formats and shapes.
- Redundant content is prevalent across these documents.
- An agent needs accurate information that can be cited.
- Knowledge changes frequently, so files need to be refreshed and reindexed.

**Interactions**

The content cannot be ingested or used by the agent as is. The content needs to be chunked, embedded, stored in a vector database, and indexed before it can be retrieved and used by agents.

**Ingest and prepare**

1. **Crawl and ingest sources:** Sources can be identified in two ways: manually, such as uploading a PDF file, or by their location, such as AWS S3.
2. **Chunking:** The ingested content is broken down into smaller, manageable chunks to facilitate efficient processing and retrieval. This is a critical step for RAG, as it ensures that only the most relevant pieces of information are retrieved, rather than entire documents.
3. **Embedding:** Each chunk is then converted into a numerical representation called an *embedding* using a specialized language model. These embeddings capture the semantic meaning of the text, allowing for similarity-based searches.
4. **Vector storage:** The embeddings are stored in a Data 360 vector store, a specialized database optimized for high-performance similarity searches. This allows the agent to quickly find related content.
5. **Indexing:** The content and its embeddings are indexed within the vector store, making them readily searchable for retrieval.

**Data 360 retriever functions**

- **Retrieve content:** This function takes a query as input and performs a semantic search against the Data 360 vector store to find the most relevant content chunks.
- **Filter content:** This function allows for filtering retrieved content based on metadata, such as document type, author, or date, to further refine results.
- **Rank content:** This function ranks the retrieved content chunks based on their similarity score (vector search), keyword score, or a combination of both (hybrid search).

**Retrieve and generate**

- **Query:** When an agent needs information, it formulates a query that is also embedded into a vector.
- **Semantic search:** The agent performs a semantic search against the Data 360 vector store, comparing the query's embedding to the embeddings of the stored content chunks. This retrieves the most semantically relevant chunks based on vector score or hybrid score (vector and keyword combined).
- **Retrieval-augmented generation (RAG):** The retrieved content chunks are then provided as context to Agentforce Agents along with the original query. The LLM uses this context to generate a precise, accurate, and citable answer.
- **Response and citation:** The agent presents the generated answer, often with citations to the original source documents or web links, to build trust and allow for verification.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Accuracy | Higher trust (grounded answers with citation) | Document curation and hygiene |
| Retrieval | Handles natural language and keywords | More storage, tuning effort |
| Security | Can enforce privileged access | Runtime overhead, cache complexity |
| Chunking | Better relevance | More preprocessing and tuning |
| Versioning | Filters outdated knowledge | Maintenance and governance costs |

**Recipe 2: Data Graphs: Pre-Curated Structured Graph Data for Agents**

**Problem**

Organizations frequently possess siloed relationship data that hinders an agent's ability to retrieve it. This issue frequently results in agents providing incomplete responses that lack sufficient contextual detail to build trust about how different entities are connected, or causes delays when agents must retrieve information from multiple databases.

**Pattern**

This pattern provides the architecture for enabling agents to ingest and interpret a wide variety of structured and semi-structured relationship information, from internal CRM data to external knowledge graphs. Giving an agent access to this data is the key to unlocking advanced capabilities like customer 360 views, complex dependency analysis, and dynamic context building.

**Context**

1. Relationship data is scattered across various systems and formats.
2. Agents need to understand connections between entities (for example, a customer, their cases, their orders, and related products).
3. Knowledge graphs and connected data models are essential for understanding complex relationships.
4. The agent needs accurate information about entity relationships that can be cited.

**Interactions**

The relational data needs to be harmonized and represented in a graph structure before it can be effectively queried and used by agents.

**Ingest and prepare**

1. **Crawland ingest sources:** Data sources (for example, CRM systems, ERPs, external APIs, and CSVs) are identified and ingested into Data 360.
2. **Data harmonization:** Raw data is mapped to Data Model Objects (DMOs) within Data 360, standardizing its structure and creating a unified view.
3. **Identity resolution:** Duplicate customer profiles are consolidated and related records are linked to create a single, accurate view of each customer.
4. **Data Graph Creation:** DMOs are connected to form a data graph, representing relationships between different entities (for example, a customer DMO is connected to a case DMO, which is connected to a product DMO). This graph allows for efficient traversal of relationships.
5. **Calculated Insights:** Aggregate metrics and derived attributes (for example, a customer's total purchase history) are calculated and added to the data graph for richer context.

**Retrieve and generate**

1. **Query:** When an agent needs information involving relationships between entities, it formulates a query against the data graph (for example, "What are all open cases for this customer and what products are associated with them?").
2. **Graph traversal and Query API:** The agent uses the Data 360 Query API to traverse the data graph and retrieve connected records, calculated insights, and relevant attributes based on the query.
3. **Contextual generation:** The retrieved relationship-aware data is then provided as context to Agentforce Agents along with the original query. The LLM uses this enriched context to generate a precise, accurate, and citable answer that reflects the interconnectedness of the data.
4. **Response and citation:** The agent presents the generated answer, often with references to the specific records or relationships within the data graph that informed the response, to build trust and allow for verification.

**Trade-Offs**

| Aspect | Gain | Cost |
| --- | --- | --- |
| Accuracy | Higher trust (grounded answers with verifiable relations) | Data harmonization and graph modeling effort |
| Retrieval | Handles complex relational queries | Graph traversal can be computationally expensive for very large graphs |
| Security | Can enforce privileged access based on relationships | Runtime overhead, complex access control |
| Context Depth | Rich, holistic understanding of entities and their connections | More preprocessing and tuning for graph optimization |
| Maintainability | Centralized data model for relationships | Continuous alignment of DMOs with evolving business needs |

The enterprise stands at the edge of a new era of automation and intelligence, led by AI agents. From handling simple customer queries to autonomously executing complex business strategies, agents promise to redefine productivity and customer engagement. The Salesforce Agentforce platform offers the essential, trusted foundation for this transformation. With a robust suite of declarative and pro-code tools, a unified data platform, and commitment to open standards through A2A and MCP, Agentforce provides a comprehensive and trusted foundation to build every type of agent. This architecture allows organizations to deploy intelligent, goal-oriented agents that act as connected partners, not in isolation, to drive measurable business success.

Salesforce provides a powerful, integrated set of tools, unified by the Agentforce platform, that serve as the foundation for building sophisticated agents. The recipes and examples in this document assume familiarity with the capabilities of the Agentforce platform and how agents interoperate. This section offers a refresher on the key components you need to understand to get the most out of the recipes and patterns in this document.

This section outlines the foundational platform capabilities that are essential for architects and developers building agents on Agentforce.

- **Salesforce Flow:** The primary tool for defining agent logic. Its declarative, visual interface is ideal for orchestrating the steps an agent will take.
- **Apex:** Provides the power for complex custom logic, state management for autonomous agents, and intricate integrations
- **Platform Events:** The nervous system for proactive and collaborative agents, serving as the transport layer for the A2A protocol.
- **Data 360:** The agent's unified, long-term memory. It provides the context necessary for intelligent action and is the foundation for retrieval-augmented generation (RAG).
- **MuleSoft:** The agent's bridge to the outside world, enabling both system integration and cross-platform agent communication via MCP.
- **Slack:** A primary surface for human–agent interaction, including tasking, notifications, and approvals
- **Agentforce Chat Client:** The customizable, embeddable front-end for customer-facing conversational agents

For agents to be truly effective, they cannot exist in a silo. Agentforce embraces two core interoperability patterns:

- **Agent2Agent (A2A) communication:** This protocol governs how agents within the Salesforce ecosystem communicate with each other. The Agentforce platform acts as both an **A2A client and a server,** making and listening for requests, respectively, which is crucial for collaborative agent swarms. Agents can be configured with **related agents** to discover and invoke other agents with specific skills, creating a dynamic and extensible system. Platform events serve as the durable, asynchronous transport mechanism for these A2A messages.
- **Model Context Protocol (MCP):** This [standard](https://modelcontextprotocol.io/docs/getting-started/intro) ensures that agents are not locked into a single platform. MCP defines a common message format that allows agents built on different frameworks to communicate. In this model, **Agentforce acts as an MCP client.** For example, a Salesforce agent could query an external agent specializing in complex logistics calculations by sending it an MCP-compliant request. MuleSoft serves as the gateway, transforming the internal A2A request into an external MCP-formatted API call, ensuring seamless interoperability across the enterprise.