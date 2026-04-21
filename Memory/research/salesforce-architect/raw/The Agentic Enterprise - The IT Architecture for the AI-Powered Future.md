This document presents a point of view describing the IT architecture that enterprises will need over the next 3-5 years to fully capture the value of an agentic workforce; it outlines the IT transformation required to support the large-scale deployment of AI agents. The goal is to provide a strategic guide and reference architecture to help CIOs, CDOs, and IT leaders plan their journey toward becoming an Agentic Enterprise.

Powerful AI models are enabling the creation of an agentic workforce capable of sensing the environment, reasoning about data, making autonomous decisions, performing tasks, and effectively collaborating with human workers. This new workforce promises a step-change in innovation, productivity, and agility, creating value for shareholders and customers. To realize this vision, organizations must undergo a business and IT transformation to become Agentic Enterprises.

Today, the traditional enterprise faces operational inefficiencies arising from information siloes, employees buried in manual work, misaligned incentives in organizational structures, and disjointed feedback loops between strategies and outcomes. These issues lead to suboptimal customer experiences, inefficient processes, and missed opportunities for growth.

The Agentic Enterprise overcomes these limitations by integrating a digital workforce of intelligent AI agents with human workers. With this new AI-augmented workforce, an organization can foster innovation for growth, drive operating excellence, and build enterprise resilience with several types of new business capabilities.

**New business capabilities to foster innovation:**

- Augmented Human Productivity: The speed, scale, and always-on nature of AI agents allows enterprises to automate repetitive work, and free human workers to focus on higher-value and more creative tasks.
- Adaptive Capability Improvement: Because the reasoning of AI agents can be observed, they can dynamically learn and deploy new skills, enabling the enterprise to continuously improve performance to meet business goals and adapt quickly to new market opportunities.

*Example in Action — Innovating the Customer Experience in financial services:* A wealth management firm can use an AI agent to reinvent its client engagement model. The agent autonomously monitors portfolios, identifies key moments for a client review, and prepares the pre-call plan for the advisor, adjusting the plan as news emerges. This allows the human advisor to deliver a proactive, personalized customer experience at scale, strengthening relationships and uncovering new opportunities.

**New business capabilities to protect and ensure organizational resiliency:**

- Elastic Workforce Capacity: Enterprises can quickly scale their ability to meet surges in workload from changing business conditions, without the costs and delays of ramping up a entirely human workforce.
- Predictive Operational Resilience: The 24/7 nature of AI agents enables them to autonomously anticipate, model, and mitigate operational, compliance, and security risks in real-time, ensuring the enterprise maintains the trust of its customers and stakeholders.

*Example in Action — Protecting customer data:* A large enterprise can deploy an AI data governance agent to scan the regulatory environment for changes in data privacy laws, discover and classify sensitive information in enterprise data sets, and then apply the appropriate governance policy. The agent can review data access requests and route exceptions to a human analyst for review, reducing compliance risk while enabling data to be used in a trusted manner.

**New business capabilities that optimize operating excellence:**

- Autonomous Process Execution: A digital workforce can execute complex, multi-step tasks 24/7 at machine speed (with humans in the loop), reducing costs and scaling processes efficiently.
- Transboundary Orchestration: AI agents can work across the information and incentive silos that normally constrain human workers, fostering agility for cross-functional processes.

*Example in Action — Optimizing the marketing funnel in retail:* A retail marketing team can deploy an AI agent to accelerate its campaign process in response to new consumer trends. The agent can generate marketing plans, collaborate with marketing, product, and sales teams for review, and then automatically create digital collateral and execute across multiple channels, dynamically adjusting the campaign based on real-time feedback.

The IT architecture of the enterprise can be depicted using a layer construct. The layers logically group related technical functionality and facilitate structured reasoning, but do not necessarily imply specific implementations or the degree to which a layer should be designed monolithically or in a more heterogeneous manner. In this layer view (Figure 1), the traditional IT architecture consists of five main layers: Infrastructure, Data, Integration, Application, and Experience. Two cross-layers, Security and IT Operations, span these layers to ensure governance, monitoring, and protection.

The traditional IT architecture was designed for a paradigm where the enterprise’s intelligence resided with human workers who took actions in applications to access data, apply business logic, facilitate collaboration, and execute workflows. It is not designed for a paradigm where AI agents can reason and take actions for certain use cases previously done by humans (or not done at all) while humans supervise the AI agents and focus on more creative and ambiguous tasks.

![Traditional IT architecture layers diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/it-arch-1.png)

While traditional architecture may support sub-scale deployments of AI agents today, it cannot fully deliver the business capabilities of the Agentic Enterprise described above. Realizing these capabilities requires an IT architecture designed for wide-spread deployment of powerful AI agents that can address broad use cases instead of being restricted to limited deployments targeting narrow use cases.

AI agents will continue to improve over the next 5 years, and the IT architecture will need to evolve in order to realize the value of more powerful and intelligent AI agents, to become future proof. First, agents will become more intelligent as the underlying AI models (such as multi-modal LLMs) and the agents’ cognitive architectures evolve (for example, multi-step planning, task decomposition, and so on). Second, AI agents will have improved learning and adaptation abilities with memory improvements, self-reflection capabilities, and the ability to learn from feedback. Third, AI agents will have a greater ability to interact with other agents, tools, and data as evidenced by the fast evolving ecosystem of open technology standards (for example Model Context Protocol, Agent2Agent, and so on). While these three technology trends will enable AI agents to be more powerful as they execute more abstract and complex tasks, it will also introduce numerous challenges for today’s IT architecture.

First, AI agents fundamentally rely on AI models, both internally developed and externally sourced, which evolve rapidly and demand sophisticated, shared, and standardized AI/ML model management. Today, AI models are bolted on for specific use cases in an application, not as shared capabilities for reuse with common tooling for training, deployment, governance and risk management. Going forward, enterprises will need to be able to use different AI models for various agentic use cases which require tooling that enables agents to swap out underlying models (e.g., foundation model vs. domain-specific smaller model) based on business context. This necessitates managing internally developed or hosted AI models with unified lifecycle tooling to ensure consistency, reusability, scalability, and efficiency. Similarly, accessing externally hosted AI models necessitates an enterprise-wide control framework to ensure optimal performance, security, compliance, availability, and reliability.

Second, AI agents have distinct scaling patterns and operational requirements such as hosting, development, reasoning, learning, memory management, and operations, which necessitate a separate and dedicated architectural boundary for agents. Embedding this functionality directly in today’s static and deterministic application architecture would introduce unnecessary architectural complexity and risk. Moreover, AI agents should interoperate with existing applications through standardized interfaces or messaging systems for real-time interaction.

Third, AI agents need to be able to reason over disparate data sets and collaborate with each other, often across siloed application stacks, but in today’s architecture, there’s no common semantic functionality to provide a shared understanding for these agents to reason over different data sets. As a result, although single-purpose agents can be deployed successfully, scaling them to operate in large numbers on complex, cross-silo tasks remains difficult and risky.

Lastly, the current enterprise IT architecture lacks an effective way to orchestrate, optimize, and govern end-to-end business processes that include the dynamic workflows performed by more powerful agents, which will augment and in some cases replace the role done by human workers in that process. Today, automation tools are leveraged to manage linear, deterministic workflows that typically follow a predefined sequence, documented in process-specific languages, and rely on static logic that rarely changes. AI technologies can enhance some of these linear processes (for example, using ML models instead of hardcoded business rules to calculate loan approval thresholds), but the strategic and execution aspects of most critical business processes remain inherently dynamic and flexible. Tasks such as developing marketing strategies, resolving complex customer issues, or prospecting clients have clear objectives (customer satisfaction, case resolution speed, and so on) but do not follow a fixed, predefined sequence of execution.

Currently, traditional enterprises primarily rely on humans to coordinate and perform these complex business processes (such as setting strategy and managing complex programs). As AI agents continue to evolve (greater intelligence, learning, and interaction capabilities) over the next 3-5 years, their ability to execute such dynamic processes autonomously will significantly expand, introducing complexities and integration challenges far exceeding the capabilities of existing integration and automation tools. The adaptive and dynamic nature of AI agents creates a strong need for novel orchestration capabilities to ensure enterprise-level control, comprehensive visibility, and consistent alignment with enterprise-wide strategic objectives, particularly in managing complex, lengthy, and multi-step workflows that encompass AI agents, humans, automation tools, and other deterministic systems.

The IT architecture of the Agentic Enterprise establishes a platform for intelligent actions by seamlessly integrating human workers, AI agents, and deterministic systems. This architecture empowers both human and AI agents to dynamically access and leverage unified enterprise knowledge from diverse data sources, enriched with semantic context to efficiently execute complex workflows and processes aligned with strategic business goals. The existing IT architecture of a set of siloed platforms and point solutions will evolve towards a set of composable application services, semantic and data tools, and networks of AI agents overseen and governed by new intelligent business process orchestration tools.

This architecture enables agents to sense, reason, and act within their respective scopes, work within and across business domains, and continuously learn, improve, and adapt. This necessitates a design focused on robust mechanisms to access data and knowledge (semantic understanding), flexible and standardized communication protocols and interfaces (such as agent to agent, agent to deterministic systems, and agent to human) and critically, orchestrate workflows and processes across agents, humans, and automation tools and deterministic systems.

To realize the architectural vision of a platform for intelligent actions, these design principles are recommended as best practice:

- **Composability and modularity:** Design architectural elements as modular components with standardized interfaces to enable rapid and dynamic assembly of agent capabilities, workflows, and human facing surfaces. Prioritize clear interface contracts and abstraction to enable the greatest flexibility for AI agents to compose workflows.
- **Data and semantic first:** Ensure comprehensive, accurate, fast, secure, and cost-effective access to data, with shared semantic understanding for agents to effectively reason across siloed systems. This requires treating data (and metadata) as a product, with tools to ensure quality, lineage, governance, and access as well as a way to provide semantic understanding shared across agents and humans.
- **IT and business observability embedded:** Embed end-to-end monitoring, tracing, evaluation, and explainability capabilities within the entire architecture for insight into agents’ reasoning, behaviors, system interactions, and impact on business KPIs to enable the continuous optimization of agents’ performance. This includes cost optimization (FinOps), sustainability metrics, and operational telemetry while maintaining trust, compliance, and responsible resource consumption. Since AI agents are inherently non-deterministic, observability is paramount to ensure AI agents can operate in a trusted, compliant, and auditable manner with human oversight.
- **Trust-throughout:** Enforce dynamic, granular permissions based on the intent of the agent’s tasks (data access, actions, and so on) and implement comprehensive security practices including red teaming, automated CVE scanning, vulnerability detection, and risk-based validation controls. More granular and dynamic controls are needed given the risk of agents causing cascading risks due to their ability to operate at machine speeds. Ensure all AI-generated outputs (from agents or models) are rigorously validated against defined policies for compliance, safety, toxicity, and bias before use or delivery, requiring logging and explainability mechanisms with verifiable audit trails for AI decisions, actions, content, and predictions.
- **Agent-first with human oversight:** Enable AI agents to be the default tool to solve business use cases, barring other considerations (e.g., cost, technical fit), and design IT systems to be accessible for agentic workflows. This includes the ability for humans to monitor, intervene in, and override any step of an agent's process. Agents require self-reflective capabilities to proactively seek human guidance if its confidence over decision-making falls below pre-programmed thresholds.
- **Reactive and multimodal interaction:** Enable the architecture to support comprehensive agent invocation and response mechanisms across all interaction types including agent-to-agent protocols, human multimodal inputs (voice, text, visual), business events, system signals, and streaming data. Enable both event-driven and real-time processing capabilities to ensure agents can react to any timely signal from any source or format.
- **AI-ready infrastructure:** Ensure infrastructure can elastically scale with redundancy built in to handle fluctuating AI workloads, and integrate ML/LLM pipelines into data and application architecture, while maintaining compliance with data residency requirements.
- **Open ecosystem:** Prioritize interoperability and avoid technology lock-in by favoring open standards, protocols, and well-defined interfaces (APIs, events) to benefit from the technology ecosystem.

To successfully enable and scale the agentic transformation, enterprises must go beyond merely enhancing current layers; they need to consider explicitly introducing four additional architectural layers (Figure 2) designed specifically to meet the needs of AI agents.

The **Agentic Layer** is dedicated to the development and management of AI agents, encompassing cognitive capabilities such as planning, reasoning, memory, tool utilization, state management, and lifecycle control. This layer addresses the unique technical and operational requirements of AI agents, ensures interoperability across applications and data stores through standardized protocols, and facilitates agent-to-agent collaboration. The existing application layer will evolve into application services to be dynamically composed for agentic workflows.

![Architecture layers diagram showing the 11 layers of the Agentic Enterprise](https://a.sfdcstatic.com/developer-website/prod/images/architect/it-arch-2.png)

The **Semantic Layer** is introduced to resolve the disconnect between raw enterprise data and the semantic understanding that AI agents need. It explicitly encodes and manages business entities, concepts, definitions, and inter-relationships, creating an enterprise ontology and representation of business knowledge to enable shared semantic understanding that power more complex multi-agent workflows performing higher-level tasks. Beyond a data catalog, the Semantic Layer translates a natural language query into precise queries against specific data stores, harmonizes the results, and returns a contextual and richer answer for the agent. The existing Data Layer meanwhile unifies via adoption of centralized lakehouses while broadening data access via an AI-ready data fabric to support data mesh operating model principles.

The **AI/ML Layer** centralizes the management of enterprise AI capabilities, including large language models, large action models and domain-specific ML models, handling both internally developed AI models throughout their lifecycle and the controlled access/usage to external AI services. Unlike traditional architectures where AI models are embedded within applications, this layer establishes AI models as first-class components and shared services in the enterprise. It focuses on enterprise-controlled AI capabilities (not AI capabilities provided by external vendors). This layer provides the intelligence for various agents and other AI workloads in the enterprise with standardized mechanisms for trust, safety, compliance, and deployment.

The **Enterprise Orchestration Layer** is the functional abstraction for coordinating, governing, and optimizing complex, multi-step workflows and business processes that span AI agents, humans, automation tools, and deterministic systems. This layer leverages a blended orchestration model that allows individual agents and systems to autonomously handle locally choreographed tasks using open protocols such as MCP and A2A while providing centralized end-to-end oversight and coordination of the entire process. To implement the blended orchestration model, this layer represents critical business processes in machine-legible semantically rich formats that define both the deterministic steps (modeled during design time) and the dynamic steps (decided by agents during run-time) of a business process, creating the process model foundation for governance and optimization.

Traditionally, significant portions of human-driven business processes remain undocumented or inaccessible in machine-readable forms. However, the detailed observability of AI agents’ activities including rich data and metadata about their tasks and actions enables capturing, documenting, and integrating dynamic, previously unstructured work with deterministic linear workflows to create comprehensive process models. The detailed process documentation captures previously invisible task interdependencies and execution paths, enabling the enterprise to continuously optimize operational efficiency, effectively address bottlenecks, and systematically codify agent-identified best practices into reusable enterprise-wide playbooks. This results in a holistic digital twin of individual processes, and when scaled, the entire enterprise.

For example, complex processes such as executing comprehensive sales strategies, or onboarding new employees involve numerous interdependent steps where the orchestration layer can ensure appropriate levels of human involvement (e.g., exception handling), bounded autonomy for AI agents, and enforce compliance. Throughout these processes, the top-down orchestration layer adds predictability and governance, continually tracks and evaluates key performance indicators (KPIs), ensures the transactional integrity of workflows and rollback logic, and maintains visibility into every stage of the workflow to ensure alignment with overarching business objectives. To implement this functionality, this layer consumes policies, rules, and guardrails from the security and governance layer (via policy-as-code) and business goals and KPIs stored in the Semantic Layer. Given the autonomous and rapid nature of AI-driven interactions, solely relying on a decentralized choreography risks strategic misalignment or compliance violations, especially in long-running, multi-step workflows. The blended orchestration approach mitigates these risks by embedding enterprise-wide business rules, compliance checks, and policy enforcement directly into complex workflows, and integrates human oversight at critical junctures.

Each of these 11 layers contributes specific functionality to deploying AI agents at scale in a secure, trusted, and effective way that unlocks the full potential of agentic AI to transform how work gets done in an enterprise. The below section outlines the layer’s function, novel changes due to the rise of AI agents, and its key technology capabilities.

**Function:** The Experience Layer serves as the primary interface for human users, enabling multimodal interaction by capturing inputs (text, voice, visual) and delivering contextually relevant responses across multiple devices. It seamlessly hands off user intentions to the Agentic Layer for action while also providing the dynamic UI and visualizations that facilitate human escalations and approvals within agentic workflows.

**What’s different vs today:** AI will augment traditional GUI-based interfaces with natural language processing, contextual awareness, and proactive decision support. AI agents will be able to proactively initiate interactions, delivering personalized, real-time recommendations across all channels and modalities.

**Key technology capabilities:**

- **Conversational AI & Digital Assistants:** Enable the UX by default to feature AI assistance to support human users.
- **Attribution & Transparency UI:** Make responses explainable in the user interface such as showing citations, sources of files/systems, and the approach/rationale on the decisions.
- **Proactive & Ambient Notification Service:** Enables agents to proactively push insights or alerts to users on the most appropriate channel and form factor, based on the user's current context.
- **Omnichannel Experiences:** Provides a seamless, consistent, and unified experience across all channels with journey continuity, where conversations and tasks follow the person instead of the app.
- **Multi-Modal Capabilities:** Allows humans to interact with agents and applications via text, voice, image, touch, video, and AR/VR so agents can understand and present information in the most efficient modality.
- **Context-Aware Personalization & Dynamic UI:** Enables contextually aware real-time (time, location, user actions) user experiences to enable personalization, including UI generation on the fly.

**Function:** The Agentic Layer acts as the default runtime environment for doing work in the enterprise where AI agents decompose tasks from the experience layer and execute tasks by dynamically assembling workflows using tools from the applications and app services layer and the data layer. The configuration state of AI agents are stored and managed in this layer. Agents are instantiated for specific tasks, and the specific agent instances are decommissioned afterwards. This implementation enables agents to be always invoked from the latest configuration state based on offline optimizations (using functionality from AI/ML, observability, and orchestration layers). This layer is responsible for the AI agents’ comprehensive lifecycle management, coordination, and governance.

**What’s different vs today:** This layer will emerge today’s current disparate set of pilots and limited agentic deployments. While rule-based bots exist, there are few adaptive, non-deterministic, and goal-oriented software programs deployed at scale.

**Key technology capabilities:**

- **Agent Runtime Environment:** Manages the lifecycle, execution, and resource allocation for AI agents.
- **Agent Lifecycle Management Suite:** Includes development frameworks, dev and test tooling, and management systems for agent activities and version control.
- **Agent Reasoning Engine:** A cognitive framework for agents to decompose goals, plan, and decide what tools to use to solve complex problems.
- **Agent Memory and Context Store:** Allows agent instances to recall and maintain context about previous interactions, ensuring consistency and personalization.
- **Agent Interoperability Protocols:** Standardized interfaces for agent-to-agent communication (A2A) and for agents to interface with external systems (such as via the Model Context Protocol).
- **Tool Registry:** A curated set of internal and externally supported tools for agents to invoke to accomplish a particular task.
- **Agent Registry:** A curated ecosystem of pre-built AI solutions and agents that supports discovery and capability matching.
- **Distributed Agent Policy Enforcement:** Enables enterprise-wide governance by allowing agents to self-check compliance before taking actions.
- **Agent Self-Reflection & Adaptation Framework:** Provides a mechanism for an agent to analyze its own performance and, with human approval, trigger improvements or suggest modifications to itself.

**Function:** This layer functions as a centralized intelligence hub, offering AI models as a set of shared services to be consumed by the Agentic Layer (and applications) to power its reasoning and decision-making capabilities with safety frameworks and monitoring built-in.

**What’s different vs today:** Traditionally, AI models were embedded within specific applications. In the IT architecture of the Agentic Enterprise, the AI/ML layer will be a first-class, centralized set of services that power many applications and agents, supporting the entire model lifecycle from development to real-time serving at scale.

**Key technology capabilities:**

- **Pre-built Foundation Models:** Large ML models trained on a broad spectrum of data, capable of performing a wide variety of general tasks.
- **Retrieval-Augmented Generation (RAG):** An AI-centric pipeline that grounds foundation models in enterprise-specific data to improve accuracy and reduce hallucinations.
- **AI Trust, Safety, & Governance Hub:** A suite of tools integrated into the model lifecycle to enforce responsible AI principles like bias detection, explainability, and safety monitoring.
- **Model Gateway:** A routing engine that acts as a single entry point for all model inference requests, managing calls to various internal and external models to optimize for cost, performance, and compliance.
- **Model Development Workbench:** An integrated development environment for data scientists with tools for data preprocessing, model training, and experimentation.
- **MLOps & Lifecycle Automation Pipeline:** The CI/CD engine for machine learning, automating the end-to-end lifecycle of models from training to deployment and retirement.
- **Model Serving & Inference Runtime:** A scalable and low-latency environment for deploying trained models as secure API endpoints for real-time consumption.
- **Model & Asset Registry:** A centralized, version-controlled repository for all AI/ML assets, including models, datasets, and source code, ensuring reproducibility and auditability.
- **Synthetic Data Generation and Management:** Tooling to generate and manage synthetic data that maintains the statistical properties of real data without exposing sensitive information.

**Function:** The Enterprise Orchestration Layer is the control plane for end-to-end work in an agentic enterprise. It ensures that agentic workflows and interactions adhere to enterprise objectives and governance policies. It consumes observability telemetry from other layers to build comprehensive business process models, enabling optimization against KPIs drawn from the Semantic Layer. This layer provides the shared context and long-running memory to each new instance of an AI agent for critical workflows.

**What’s different vs today:** This layer provides unified visibility into business processes by creating machine-legible models that capture both structured, deterministic steps, and the unstructured, dynamic work performed by humans and agents. It moves beyond today’s human-centric collaboration and governance models by programmatically encoding business objectives and compliance rules as constraints into agentic workflows to govern the agentic workforce.

**Key technology capabilities:**

- **Hybrid Workflow Execution Engine:** The core runtime that executes the "blended orchestration model," providing centralized oversight while allowing for local agent choreography.
- **Process Governance & Constraint Engine:** A real-time governance service that consumes and applies declarative business rules, policies, and constraints to all in-flight processes.
- **Shared Memory and Context Management:** A shared memory layer accessible to all actors in a workflow to maintain continuity and coherence across multiple steps.
- **Process Modeling Studio:** A design-time environment for creating and managing machine-legible, semantically rich process models that define both deterministic and dynamic, goal-oriented steps.
- **Process Optimization and Simulation:** A capability that constructs digital simulations of business processes for advanced analysis, what-if simulations, and predictive optimization.
- **Process Discovery & Health Monitoring:** Ingests process models and real-time data to report on business metrics of process health.
- **Digital Twin Process Modeling:** A real-time mirror of live workflows for testing, simulating changes, and optimizing without impacting production.

**Function:** This layer exposes existing business application functionality as composable and modular tools and services for agents to use. It also serves as the presentation runtime for embedding agentic capabilities into the user experience. Applications continue to be the system of record but are re-engineered to be "headless" capabilities for agents.

**What’s different vs today:** Applications will evolve from monolithic UIs to "back-end services" that agents can dynamically call via APIs and events. This layer will be natively integrated with AI agents and models, and the proliferation of code-generation LLMs will lead to an increase in the number of custom, agent-built micro-applications.

**Key technology capabilities:**

- **Modular Application Services:** Decomposed business logic from traditional applications, published as machine-readable actions for agents to call.
- **Agent Embedding SDKs:** Toolkits and libraries that enable developers to securely embed agents directly into application UIs.
- **Dynamic UI Generation Services:** Services that allow an AI agent to generate or modify UI components in real-time based on user context.
- **AI-Native UI Frameworks:** Front-end frameworks designed with built-in support for handling AI-driven UIs, such as managing probabilistic data and streaming text responses.
- **Agent-Infused Systems of Engagement:** Enterprise productivity and collaboration applications that incorporate AI agent capabilities through visual components.
- **AI-Enhanced Low-Code / No-Code Application Development:** Tools that enable users and agents to create custom apps and services using natural language and prompts.
- **App Guardrails for Agent Usage:** Application-side controls for agent usage, such as rate limiting, scoped permissions, and telemetry.

**Function:** The Semantic Layer provides a unified understanding of data and knowledge across the enterprise, enabling both humans and AI agents to interpret and act on information consistently. It uses knowledge representation tools like ontologies and knowledge graphs to translate natural language queries into precise, context-aware data queries.

**What’s different vs today:** While today’s enterprises have disparate metadata stores, the IT architecture of the Agentic Enterprise requires a centralized Enterprise Knowledge Graph (EKG) that links data across domains with explicitly defined semantic relationships. This provides the rich context that AI agents can traverse to perform complex reasoning, creating requirements for a set of technical capabilities to power knowledge graphs that span multiple functional domains.

**Key technology capabilities:**

- **Metadata Service:** Provides descriptive metadata, including data lineage, ownership, and classifications.
- **Business Glossary & Taxonomy Management:** A tool for business users to define and agree upon standard business terms.
- **Semantic Model Management:** A workbench for knowledge engineers to create, manage, and govern semantic models and ontologies.
- **Enterprise Knowledge Graph (EKG):** A run-time instantiation of the enterprise ontology that stores and maps the relationships between business entities.
- **Metadata Ingestion & Harmonization Engine:** An automated pipeline that populates and maintains the Enterprise Knowledge Graph from various source systems.
- **Semantic Query Engine**: Interprets natural language queries and constructs structured queries based on the EKG to retrieve data from diverse sources.
- **Semantic Reasoning Engine:** Analyzes and derives implicit knowledge and hidden relationships from the EKG.

**Function:** The Data Layer is the foundational source of truth, managing and providing secure, governed access to all enterprise data for the Semantic Layer to interpret, the AI/ML Layer to use for training, applications to use for transactions, and agents for reasoning.

**What’s different vs today:** The Data Layer evolves to be more unified, real-time, and governance-focused, often centered on a cloud-scale data lakehouse. It must handle a greater volume and variety of data and shift from batch-oriented processing to real-time streaming to support reactive agents. Data governance and quality take on even greater importance to prevent poor data from creating flawed AI outputs.

**Key technology capabilities:**

- **VectorDB:** A specialized database optimized for storing and querying high-dimensional vector embeddings, critical for RAG.
- **Intelligent Analytical Data Pipelines:** An automated, metadata-driven service for data ingestion, transformation, and loading (ETL/ELT) into the Data Layer.
- **Enterprise Data Lakehouse:** A central repository for structured, semi-structured, and unstructured data, optimized for both analytics and AI workloads.
- **Zero-Copy Data Federation & Search:** Techniques for accessing, querying, and searching data across multiple stores without physical data movement.
- **Natural Language to SQL:** A technique for converting natural language queries into SQL.
- **Enterprise Data Catalog & Discovery Service:** A centralized, searchable inventory of all data assets across the enterprise.
- **Master & Reference Data Management (MDM):** Manages the "golden record" for critical business entities like Customer and Product.
- **Adaptive Data Quality Service:** A continuous monitoring service that uses AI to automatically detect and remediate data quality issues in real time.
- **Data Contracts:** Machine-readable agreements between data producers and consumers that specify the schema, semantics, and SLAs of data exchange.
- **AI-Specialized Data Stores:** Databases designed for specific AI use cases, such as time-series or graph databases.
- **AI-Ready Data Fabric:** A logical data abstraction layer that provides a unified, virtualized view of data across disparate physical systems.
- **Real-Time Data Processing:** Capabilities for processing and analyzing multi-modal data streams continuously at machine speeds.

**Function:** The Infrastructure Layer underpins all other layers, providing the compute, storage, network, and cloud capabilities required to run AI and agentic workloads at scale in a resilient and cost-efficient manner.

**What’s different vs today:** AI workloads require greater scalability and elasticity to handle the probabilistic nature of agentic systems. Infrastructure must support rapid provisioning, specialized hardware like GPUs, and low-latency, high-throughput network traffic for inter-agent communication.

**Key technology capabilities:**

- **Infrastructure as Code:** Automated provisioning and management of infrastructure with CI/CD deployment pipelines.
- **Hybrid & Multi-Cloud AI Infrastructure:** Leverages public cloud elasticity and specialized infrastructure for generative AI workloads.
- **AI-Optimized Compute, Storage, and Network:** Dynamically allocates and scales infrastructure resources based on variable demand from AI workloads.
- **Edge AI Infrastructure:** Enables AI models and agents to be deployed at the edge of the network for use cases with unique latency or privacy requirements.
- **Self-Healing Infrastructure:** Uses AI to manage system recovery without manual input, ensuring high availability.
- **Sustainable AI Computing:** Energy-efficient approaches to mitigate the environmental impact of AI workloads.
- **Cost- & Carbon-Aware Autoscaling:** Uses FinOps and sustainability signals to drive scaling and placement of capacity.

**Function:** The Integration Layer serves as the universal communication fabric for all systems (legacy and new) through APIs, events, protocols, and middleware to ensure agents can discover and interact with services, data, and tools seamlessly.

**What’s different vs today:** Integration must evolve to support the dynamic, many-to-many communication patterns of AI agents, rather than just handling predetermined, static interactions between a few known systems. It requires real-time data processing, and must accommodate ad-hoc discovery and collaboration between agents.

**Key technology capabilities:**

- **Operational Data Connectivity Pipeline:** AI-assisted tools for automatic schema mapping, data transformation, and workflow generation, including API-led, event-driven, and Reverse ETL capabilities.
- **Adaptive API Management and Service Mesh:** API gateways and service mesh technology that can dynamically register, discover, and govern services with adaptive policy enforcement for agents.
- **Semantic Knowledge Adapters:** An integration component that provides a shared vocabulary and data model across agents and applications for consistent data interpretation.
- **Event-Driven Integration Fabric:** A high-throughput, low-latency messaging and streaming backbone that enables decoupled, asynchronous communication.
- **Agent Protocol Gateway:** A gateway for MCP services that allows agents to securely discover tools and trigger actions, bridging MCP to internal APIs and events.
- **Composable Capability Catalog & Marketplace:** A centralized, governed catalog for all enterprise capabilities—APIs, services, agent skills, models, and datasets—annotated with semantic metadata for on-demand composition.

**Function:** This layer monitors and manages the health and operational performance of agents and the entire system (observability embedded principle), providing transparency and control by generating insights to enable auditing, debugging, explainability, cost, and resource optimization of the enterprise’s agentic workforce.

**What’s different vs today**: This layer becomes even more crucial given the risk of AI agents creating errors at machine speed. It must expand beyond infrastructure monitoring to include the unpredictable behavior of autonomous agents, requiring new kinds of telemetry and the ability to understand semantic correctness, not just technical performance.

**Key technology capabilities:**

- **Real-Time Monitoring & Observability Platform:** Continuously collects logs, metrics, and traces across the entire IT environment, with extensions for ML metrics and agent behavior.
- **FinOps & Cloud Cost Management:** Responsible for monitoring, analyzing, and optimizing the infrastructure costs associated with AI and agentic workloads.
- **Agent and ML-specific Monitoring:** Logs each step of an agent's run in an immutable audit trail and continuously profiles agent behaviors to detect deviations from established norms.
- **AIOps, Incident and Change Management:** Uses AI/ML to predict potential IT issues, identify root causes, and create remediation workflows.
- **Closed Learning Feedback Loop:** Integrates observability telemetry from agents back into MLOps pipelines, enabling automated model retraining or prompt adjustment.
- **Semantic Observability Engine:** Integrates observability with the semantic layer for contextualization to enable the detection of semantic anomalies in agent behavior.

**Purpose:** This layer embeds trust and safety throughout the architecture by protecting the enterprise’s assets from threats, managing risk, and ensuring compliance with regulatory requirements. It encompasses identity management, threat detection, GRC, and AI-specific security measures.

**What’s different vs today:** The security layer must evolve to address new attack surfaces presented by AI models and agents, such as prompt injection and model poisoning. Identity and access management must shift from static, role-based controls to dynamic, intent-based permissions that are granted just-in-time and revoked immediately after use.

**Key technology capabilities:**

- **LLM Input/Output Security & Guardrails:** Enterprise guardrails applied at prompt and response time to block unsafe content, PII leaks, and jailbreaks.
- **Zero Trust Architecture with AI Verification:** Continuous authentication enhanced by AI-based behavioral analysis, with granular, just-in-time access for agents based on their specific task.
- **Agent Security Framework:** Fine-grained permission models, monitoring for harmful behaviors, and containment mechanisms to safely interrupt agent activities.
- **AI Model Security:** A defense-in-depth strategy with controls at each stage of the model lifecycle to protect against poisoning, extraction, and adversarial attacks.
- **Privacy-Preserving AI:** Techniques such as federated learning and differential privacy to protect sensitive data.
- **AI-Enhanced GRC:** Use of AI agents to continuously monitor IT architecture compliance with controls.
- **Policy-as-Code Engine:** A single source of truth for defining business rules and compliance constraints in a declarative, machine-readable format to set guardrails for agent behavior.
- **Continuous Red-Teaming:** Automated, ongoing adversarial testing of AI models and agents to identify vulnerabilities before attackers exploit them.

Transforming into Agentic Enterprise requires following a multi-stage journey by setting the technology foundations while creating tangible business value (see Figure 3 below). While the precise roadmap depends on the enterprise’s strategy, culture, AI governance model and IT architectural starting point, most organizations should adopt a phased approach as continued IT investments power agents with growing scope, complexity, and value creation. Salesforce’s [Agentic Maturity Model](https://www.salesforce.com/news/stories/agentic-maturity-model/) offers a useful framework of maturity levels for enterprises to strategize their transformation, outlining how agent capabilities can grow from basic informational retrieval (level 1) to orchestrating more complex multi-domain (level 2 and 3) and multi-agent workflows (level 4). To successfully advance through these stages, the IT architecture must evolve in a concerted manner, with targeted investments in different layers of the architecture at each phase to meet the needs of the more complex and higher-value deployments of AI agents. For each maturity level, the specific technology capabilities required across the 11 architectural layers are identified with a rationale for investment.

![Roadmap diagram showing maturity levels 1-4](https://a.sfdcstatic.com/developer-website/prod/images/architect/it-arch-3.png)

**Maturity Level 1: Information Retrieval Agents**

**Business Objective & Value: Enhance human worker productivity by providing a trusted, conversational interface for querying enterprise knowledge.** The primary value is in augmenting human capabilities, not replacing them. These agents assist humans by retrieving information and recommending actions.

**Architectural Focus:** The focus is on establishing a secure, reliable data foundation and the basic AI components needed for information retrieval. Governance and observability are critical from day one to build user trust and to control costs.

**Key Technology Investments (Figure 4):**

At this stage, IT should focus on creating a trustworthy data-to-agent pipeline and other foundation capabilities. Technologies in the **Data Layer**, such as a **VectorDB**, are essential for enabling the retrieval augmented generation (RAG) techniques that powers information retrieval agents. This is coupled with a centralized **AI/ML Layer** that includes a **Model Gateway** for secure, cost-controlled access to foundation models and an **AI Trust, Safety & Governance Hub** to monitor for unsafe outputs and ensure compliance. **Master data management** and **business glossaries** in the **Semantic** **Layer** are foundational for agents to retrieve accurate information. Agent runtime and lifecycle capabilities are required to ensure agents built in this stage can be modified and extended for future use cases. To deliver value and build user confidence, the **Experience Layer** must incorporate an **Attribution & Transparency UI**, which makes agent responses explainable by showing citations and the sources of its information. Foundational observability and security investments (for example **zero** **trust**) must begin implementation to set the stage for future agentic deployments.

![Technology investment diagram for Maturity Level 1](https://a.sfdcstatic.com/developer-website/prod/images/architect/it-arch-4.png)

**Maturity Level 2: Simple Orchestration, Single Domain Agents**

**Business Objective & Value: Automate routine tasks and orchestrate low-complexity workflows within a single business domain.** This improves operational efficiency and reduces manual work, allowing human workers to focus on higher-value activities.

**Architectural Focus:** The key architectural shift is from read-only data retrieval to executing actions. This requires beginning a longer journey to modularize application functionality (often exposed as APIs) for agents to access, implementing robust security for agent actions, and building semantic and AI development functionality to further the intelligence of AI agents.

**Key Technology Investments (Figure 5):**

Investments thematically center on enabling AI agents to take action with proper governance in place. The **Applications and App Services Layer** undergoes a critical change, as monolithic business logic is decomposed into **modular application services** (APIs) for agents to call. These are protected by **App Guardrails** to prevent agents from overwhelming systems, with integrations into observability tooling. To power these agents, investments need to be made in agent reasoning, tool protocols (such as MCP), and **registries**. This introduces new risks, making a dedicated **Agent Security Framework and AI model and agent monitoring capabilities** essential for governance and security. Lastly, enterprises can begin scaling their AI/ML capabilities for custom models to power these agents tackling domain-specific tasks.

![Technology investment diagram for Maturity Level 2](https://a.sfdcstatic.com/developer-website/prod/images/architect/it-arch-5.png)

**Maturity Level 3: Multi-Domain Orchestration Agents**

**Business Objective & Value:** **Automate complex, end-to-end business processes that span organizational and functional boundaries** (such as "quote-to-cash", “lead to order”). The value is in breaking down silos, accelerating process cycle times, and optimizing entire value chains within the business. Higher step changes in human worker productivity are possible as organizational barriers begin to break down and humans begin to focus more on overseeing AI agents.

**Architectural Focus:** The architecture must now support cross-cutting technical issues. A shared semantic understanding across the enterprise, a centralized orchestration engine for governance, and a decoupled, event-driven integration fabric become the critical enablers.

![Technology investment diagram for Maturity Level 3](https://a.sfdcstatic.com/developer-website/prod/images/architect/it-arch-6.png)

**Key Technology Investments (Figure 6):**

Technology investments are thematically focused on orchestrating processes at an enterprise scale across humans, agents, and deterministic systems. The **Enterprise Orchestration Layer** becomes a focus of investment, requiring a **Hybrid Workflow Execution Engine** to coordinate activities, and a **Process Governance & Constraint Engine** to enforce business rules and compliance policies on in-flight processes since agents are working across domains, often with different policies and semantic definitions. This cross-domain coordination is only possible with a mature **Semantic Layer** that features an **Enterprise Knowledge Graph (EKG)**, which creates a shared understanding of how business entities relate across domains. The **Integration Layer** must evolve to include an **Event-Driven Integration Fabric**, which uses a streaming backbone to decouple systems and enable the resilient, asynchronous communication typical of long-running enterprise processes. Given the higher value of these workflows and the associated risks, additional investments in security and monitoring become paramount (for example **AIOps, policy-as-code**). Lastly, further investment must be made in the Application and Services Layer (such as **AI-enabled LCNC, more dynamic and multi-modal** user experiences) as human users begin to monitor and collaborate with more capable AI agents.

**Maturity Level 4: Multi-Agent, Multi-Domain Orchestration**

**Business Objective & Value: Redesign and optimize business operations across domains to drive step changes in productivity and efficiency.** This stage moves toward creating a holistic digital simulation (digital twin) of the enterprise for continuous improvement and strategic planning across major business processes and workflows.

**Architectural Focus:** The final stage focuses on enabling dynamic, emergent collaboration between agents. This requires advanced agent-to-agent (A2A) communication protocols, agent self-learning capabilities, further investing in maturing the Orchestration, Data, and Semantic layers, and fully dynamic and self-healing infrastructure to support the growing needs of dynamic AI workloads as agents have been scaled out across the enterprise.

![Technology investment diagram for Maturity Level 4](https://a.sfdcstatic.com/developer-website/prod/images/architect/it-arch-7.png)

**Key Technology Investments (Figure 7):**

Thematic investments focus on creating a self-improving, autonomous system. In the **Agentic Layer**, an **Agent Self-Reflection & Adaptation Framework** provides the mechanism for an agent to analyze its own performance logs and trigger improvements. This learning is supported by the **IT Operations and Observability Layer**, which implements a **Closed Learning Feedback Loop** to automatically feed observability data back into MLOps pipelines for model retraining which can also leverage synthetic data generation to further optimize model performance. With networks of agents being deployed across departments along with ongoing application modularization efforts, further investments in security and crucially a **composable capability catalog** become necessary for agents to dynamically compose capabilities to solve more abstract and higher-value tasks. These processes are all orchestrated and optimized via a new **Digital Twin Process Modeling capability,** which uses real-time data to create simulations for "what-if" analysis and predictive optimization, allowing the enterprise to safely test and deploy new agentic deployments.

**Conclusion**

The roadmap to an Agentic Enterprise runs through an IT architectural evolution. Enterprise architects will be the crucial drivers of this transformation, driving the critical investment decisions, along with other partners in the business and IT, necessary for the organization to realize the value from the new business capabilities of the Agentic Enterprise.