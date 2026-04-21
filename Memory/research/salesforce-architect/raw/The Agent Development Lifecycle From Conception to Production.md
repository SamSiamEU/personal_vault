In traditional software development, the Software Development Lifecycle (SDLC) provides a structured, phased approach to building applications. It establishes quality, reduces risk, and provides a clear roadmap from idea to release. The Agent Development Lifecycle (ADLC) is a similar methodology that’s distinctly tailored to address the unique complexities of building autonomous agents.

Agents aren’t passive applications; they’re systems that reason, act, and learn within dynamic execution environments. Their non‑deterministic behavior makes traditional QA insufficient. The Agent Development Lifecycle (ADLC), championed by platforms like Agentforce, addresses this across five phases: Ideation and Design, Development (the “inner loop”), Testing and Validation, Deployment, and continuous Monitoring and Tuning (the “outer loop”).

This document serves as a comprehensive guide for developers and Enterprise Architects who are already familiar with the intricacies of the Software Development Lifecycle (SDLC) and are looking to expand their expertise into agent-based systems. Our primary objective is to facilitate a rapid understanding of the Agent Development Lifecycle (ADLC) by highlighting its key distinctions from traditional SDLC methodologies and providing a structured framework for conceptualizing the entire process of building, deploying, and managing intelligent agents.

The document is organized into three distinct chapters, each designed to progressively build your knowledge and practical skills:

- **Chapter 1: The ADLC Framework.** This chapter introduces the Agent Development Lifecycle (ADLC), detailing its divergence from the SDLC due to the unique challenges of developing autonomous agents. It establishes a framework for designing, developing, testing, and deploying agents.
- **Chapter 2: The Agentforce Platform.** This chapter explores Agentforce, a unified platform that streamlines and accelerates the entire Agent Development Lifecycle. Agentforce offers tools for agent design, data processing, model training, deployment, and continuous monitoring, simplifying complex tasks and improving efficiency.
- **Chapter 3: Pro-Code Implementation.** This guide uses Agentforce's pro-code tools to provide practical, step-by-step instructions and real-world examples for agent development. It covers the entire Agent Development Lifecycle, from prototyping and feature engineering to model deployment, performance tuning, and maintenance, equipping developers with the skills to build production-ready agents.

This document aims to equip you with the theoretical and practical knowledge of Agentforce's pro-code tools. You will learn to build, deploy, and monitor agents efficiently, safely, and reliably, gaining a comprehensive understanding of the ADLC and maximizing Agentforce's potential in intelligent agent development.

The non-deterministic nature of AI agents requires a specialized development framework. This chapter outlines that framework by introducing the Agent Development Lifecycle (ADLC). This chapter provides a comprehensive overview of the five core phases of the ADLC, from initial Ideation and Design to continuous Monitoring and Tuning. This chapter establishes the foundational knowledge required for building robust and reliable agents.

This section maps SDLC concepts to the five phases of the ADLC.

This is the foundational phase where an agent's strategic purpose and operational boundaries are defined. A well-structured design phase is the most critical step for success, as it translates a business need into a technical blueprint. The design process ensures that the agent is not only functional but also responsible and aligned with user expectations. It is where the "what" and "why" are established before any code is written.

1. **Define Agentic Goals and Capabilities**: First, you must clearly articulate the agent’s primary objective and the specific, measurable tasks it will perform. This involves defining its role (e.g., "customer service assistant"), its core functions (e.g., "booking appointments," "answering product questions"), and the success metrics for each.
2. **Establish Persona and Ethical Guardrails**: This step involves designing the agent's personality and defining its ethical boundaries to ensure it is trustworthy and safe. It establishes the agent’s tone (e.g., "formal," "friendly") and implements strict rules to prevent harmful, biased, or inappropriate responses.
3. **Map Context and Understanding**: You must determine what information the agent needs to understand and remember to be effective. This includes defining the scope of its knowledge base and its conversational memory, which allows it to have coherent, multi-turn conversations.
4. **Identify Tools and System Integrations**: This involves inventorying the external systems, APIs, and data sources the agent must connect with to execute tasks. Each tool (e.g., a booking API, a customer database) is identified, and its function is mapped to a specific agent capability.
5. **Plan for Human-in-the-Loop Escalation**: It is critical to define the conditions under which an agent escalates to a human. This involves reviewing potential failure points and conversational "dead ends" to determine when an agent should escalate to a human operator. The design should describe how this handoff will be performed to ensure sufficient context is transferred, so that it can be quickly consumed to ensure a seamless customer experience.

This is the hands-on construction phase where the design blueprint is turned into a functional agent. Developers build the agent, connect it to its tools, and empower it with the data it needs to perform its duties. This iterative "inner loop" of building and refining is where the agent truly comes to life.

1. **Configure the Agent's Logic and Decision-Making**: This step involves shaping the agent's reasoning by connecting its decision-making framework to context, tools and data sources. The developer's role is to define the agent's behavior by creating APIs or reusing existing APIs, setting operational guardrails, and specifying how the agent selects and uses available tools to complete complex, multi-step tasks.
2. **Engineer Prompts and Fine-Tune Models**: The agent’s persona, instructions, and constraints are codified through meticulous prompt engineering. This process involves crafting the master prompt that guides the Large Language Model (LLM) and, for more advanced use cases, fine-tuning the model on domain-specific data to improve its performance.
3. **Integrate and Secure AI Tools**: The functions and APIs identified during the design phase are connected to the agent. Using an SDK, developers wrap existing functions or create new ones, making them securely callable by the agent and ensuring they have the proper authentication and error handling.
4. **Build Data and RAG Pipelines**: To empower the agent with external knowledge, developers build the data pipelines for Retrieval-Augmented Generation (RAG). This involves connecting to and indexing data from sources like vector stores, relational databases, graph databases, or internal documents, making that information accessible to the agent for providing accurate, context-aware responses.

Testing AI agents introduces a paradigm shift from the deterministic validation of traditional software. While a conventional application is tested for correctness—a specific input must produce a single, expected output—an agent's non-deterministic nature requires a more sophisticated approach. The goal is not to validate a single right answer but to ensure the agent’s behavior is aligned with its intended purpose, is robust against unexpected inputs, and remains reliable across a spectrum of acceptable outcomes.

1. **Unit Testing**: This layer focuses on the deterministic, non-AI components of the agent. It involves traditional unit testing to validate that each individual tool and function works correctly in isolation, ensuring a reliable foundation before the agent's complex reasoning is applied.
2. **End-to-End (E2E) Testing**: This stage evaluates the agent's ability to achieve goals in realistic scenarios, which is critical given its non-deterministic nature. Instead of checking for an exact output, these end-to-end tests verify that the agent successfully completes tasks and that its performance doesn't degrade as changes are made.
3. **Adversarial and Robustness Testing**: This is the practice of intentionally trying to break the agent to proactively discover its weaknesses. Testers use ambiguous requests, malicious prompts, and other edge cases to expose vulnerabilities and ensure the agent remains resilient and safe under pressure.
4. **Human-in-the-Loop (HITL) Evaluation**: Since automated tests cannot measure nuanced qualities like tone or conversational flow, this stage relies on human feedback. Testers interact with the agent to score its responses for helpfulness and overall user experience, providing essential data for fine-tuning its behavior.
5. **Performance and Scale Testing**: This is a critical step to prevent performance bottlenecks before they impact users. This process simulates realistic peak-usage scenarios to ensure agents and applications can handle high volumes smoothly and predictably. It validates that the solution is not just correct, but also scalable.

Deploying an AI agent is a managed process focused on ensuring the validated agent is what users interact with in a reliable and repeatable way. This requires a structured approach that moves the agent from a version-controlled asset to a live, monitored service.

1. **Packaging and Version Control**: The agent's entire definition, including its prompts and tools, is captured as metadata in a file and stored in a source control system like Git. This creates a single source of truth and an auditable history of all changes.
2. **CI/CD Pipelines**: The path to production is automated to eliminate human error and ensure consistency. These pipelines automatically promote the agent through development, testing, and production environments, running end to end tests at each stage to act as a quality gate.
3. **Phased Rollout Strategies**: To minimize risk, new agent versions are released to a small subset of users first using strategies like Canary Releases. This allows for real-world performance monitoring before a full rollout, with the ability to quickly revert if any issues are found.
4. **Activation and Governance**: The critical step in rolling out an agent involves securely activating the agent with the correct permissions and ensuring it is connected to monitoring tools. This provides immediate visibility into the health and performance of the newly deployed agent from the moment it goes live.

Deployment is not the end of the Agent Development Lifecycle; it is the beginning of its continuous "outer loop." Agents are dynamic systems that operate in unpredictable, real-world environments. This phase is dedicated to observing the agent's live performance, gathering insights from its interactions, and using that data to systematically refine and improve its effectiveness, safety, and efficiency over time.

1. **Real-Time Performance Monitoring**: This is the practice of tracking the agent's key operational metrics as it interacts with users. Dashboards are used to monitor latency, token consumption (cost), and API error rates, providing an immediate, high-level view of the agent's health and efficiency.
2. **Behavioral and Success Analytics**: This involves analyzing conversational logs to understand how the agent is *actually* performing its duties. It focuses on tracking task completion rates, identifying common failure points or conversational "dead ends," and measuring user satisfaction to determine if the agent is successfully achieving its goals. As an example for Service agents it could provide metrics on how often and why an agent escalates to a human.
3. **Intelligent Tuning and Refinement**: This is the active process of using insights from monitoring to improve the agent. This can range from prompt engineering to tool optimization.
4. **Data-Driven RAG Enhancement**: The quality of the agent's knowledge base is continuously improved based on real-world queries. Monitoring may reveal that the agent is struggling with certain topics, leading to a refinement of the data sources or the retrieval process (RAG Refinement) to improve the accuracy of its responses.
5. **Continuous Learning and Adaptation**: This involves creating a feedback loop where production data is used to make the agent smarter. By labeling interaction logs—either with human oversight or LLM-based labeling—a curated dataset is built, which can be used to fine-tune the underlying model and recommend further improvements

Agentforce supports every ADLC phase with integrated tooling for design, development, testing, deployment, monitoring, and analytics— all within a single unified platform for quickly building and testing robust agents.

The Agentforce ADLC is based on the following guiding principles:

- **Built for both low-code and pro-code**: Support for configuration‑based deployment (low-code) and programmatic extensibility (pro-code).
- **Continuous AI-driven assistance & feedback loops**: Captures and analyzes conversational data to inform agent tuning for continuous AI-driven improvement.
- **Test-driven development at all levels**: Rigorous testing across all stages, validating deterministic components through traditional unit testing, and providing new approaches to testing agent reasoning and non-deterministic behavior.
- **Executive and LOB Observability**: Providing cost, usage, and performance metrics for operational and executive stakeholders.
![Agentforce ADLC Framework Diagram](https://a.sfdcstatic.com/developer-website/prod/images/architect/agent-development-lifecycle-framework-diagram.png)

This chapter shows how Agentforce supports every phase of the ADLC **within a single unified platform.**

##### Ideation

The ideation phase is the foundational stage of the ADLC, where initial vision and requirements for agents are formulated. It involves a deep dive into understanding the problem, identifying potential solutions, and outlining the core functionalities of the agent.

Start your agent's ideation process by defining its key attributes:

1. **Purpose/Goal**: Clearly define the primary objective of the agent. What specific problem is it designed to solve, or what task is it intended to accomplish? Who should the agent serve? This should be a concise and measurable statement that guides the entire development process.
2. **Persona**: Develop a detailed persona for the agent. This includes defining its identity, communication style, and the role it will play in interacting with users or other systems. Consider its tone, level of formality, and any specific characteristics that will make it effective in its intended context.
3. **Pattern**: Identify and link to relevant agentic patterns and implementation strategies. This involves architectural designs or best practices that can inform the agent's structure and behavior. " [Agentic Patterns & Implementation on Salesforce Agentforce: A Technical Whitepaper](https://architect.salesforce.com/docs/architect/fundamentals/guide/agentic-patterns)," serves as a valuable resource for this step, offering insights into effective agent design on the Salesforce platform and Agentforce.

##### Design

The design phase translates the concepts from ideation into a detailed blueprint for the agent's construction. This involves defining the agent's architecture, user flows, interaction models, and technical specifications like topics, tools, and guardrails.

During the design phase, you’ll create create a detailed blueprint for your agent's construction that includes:

- **Agent Design**: Outline the internal structure of the agent, including its components, modules, and how they interact. This might involve defining the knowledge base, configuration and logic to control agent behavior, natural language processing (NLP) components, and integration points with other systems.
- **User Flows/Interaction Design**: Map the complete user journey and the agent's interactions. Define conversation flows, decision trees, error handling, and feedback mechanisms to create intuitive, effective experiences.
- **Technical Specifications**: Document the technical non-functional requirements for the agent, such as performance metrics, scalability considerations, security protocols, and integration specifications.
- **Prototyping & Mockups**: Create visual representations or interactive prototypes of the agent's interface and interactions. This allows for early testing and feedback, helping to refine the design before full-scale development begins.
- **Data**: When determining the type and sources of data an agent requires, identify datasets, APIs, databases, and repositories the agent must access. For Agentforce, focus on what data is provided as context, whether it’s structured or unstructured, and whether it’s real‑time or batch. The Agentforce platform is built with deep integration with Data 360, allowing you to use both structured and unstructured data from Salesforce CRM and other sources. Unstructured content can be natively chunked and indexed for RAG. MuleSoft allows you to connect to external systems.
- **Tools**: Identify the actions the agent must perform. Use Agentforce Actions to expose tools that achieve business goals. These actions leverage existing Salesforce assets such as Prompts via Prompt Builder, MuleSoft, Apex, Flows, and APIs with OpenAPI specifications. Any Invocable Action can be integrated into Agentforce and used by the agent, making all familiar Salesforce development tools readily available as Agentforce Actions.
- **Input data for Agents**: In traditional SDLC, inputs are precisely specified. In the ADLC, inputs are often natural, non‑deterministic, free‑form utterances. Collect a representative corpus of utterances that are expected to produce appropriate responses.

The development phase focuses on translating the defined agent's purpose, capabilities, and operational scope determined in the Ideation and Design phase into a new Agentforce Agent.

To help developers create agents, Agentforce provides both the **Agent Builder** and **Agentforce Developer Experience (AFDX).** These foundational tools serve as the primary environments for constructing and configuring the agent.

- **Agent Builder** provides a UI experience for defining the agent’s core functionality.
- **AFDX** provides a programmatic interface for customization and integration with other systems.

Developing and building an agent involves these steps that can be performed using either the Agent Builder or AFDX:

1. **Defining the Persona**: A crucial aspect of agent design is establishing a distinct persona. This involves configuring the:
	- **Agent Description**: A detailed description of the agent's role, objectives, and the specific customer service tasks it is designed to handle.
		- **Tone**: The agent’s communication style, level of empathy, and any specific brand guidelines it needs to adhere to.
2. **Defining Agent Topics and Actions**: To make an agent sophisticated and capable of handling a diverse range of tasks it is essential to break down its capabilities into distinct topics with corresponding actions.
	- **Topics**: Each topic can be conceptualized as its own specialized agent with a unique set of instructions and tools.
		- **Modular Architecture.** The modular approach to topics allows for greater organization and scalability. By defining multiple topics, the agent can handle a wider array of complex scenarios. For example, an agent might have separate topics for "Order Management," "Frequently Asked Questions (FAQ)," "Technical Support," and "Billing Inquiries."
		- **Topic Instructions (Guardrails)**: Each topic comes with specific instructions that act as guardrails, defining the scope of what the agent can discuss or do within that topic. These instructions prevent the agent from straying off-topic or providing irrelevant information. They also help maintain consistency and accuracy in responses.
		- **Actions**: Topics are also equipped with "tools," which represent the actions the agent can take. These tools can be:
		- **Informational Actions**: Retrieving data from a knowledge base or an external system to answer a query.
				- **Transactional Actions**: Performing actions on behalf of the user, such as placing an order, updating a customer record, or initiating a refund process. These actions are often integrated with other systems (e.g., CRM, ERP).

When evaluating the performance and reliability of AI agents, testers often encounter a range of challenges that can degrade the user experience. These issues span from misinterpreting user intent to failing to execute tasks correctly.

##### Common Agent Failure Scenarios

Building a robust agent requires understanding how and where it can fail. The following table categorizes common problems encountered during the agent lifecycle, from flawed reasoning to poor knowledge retrieval. Use this as a strategic guide during development and a checklist during testing to ensure your agent is not only functional but also reliable and intuitive for the end-user. These failure scenarios should help you define test cases.

| Category | Description | Failure Examples |
| --- | --- | --- |
| Topic Classification | The agent fails to correctly identify the user's intent or goal. | - Triggers incorrect topics for given queries. - Frequently defaults to an "Off Topic" classification inappropriately. |
| Response Quality | Failures in the content, accuracy, and format of the agent's replies. | - Provides ungrounded information that is not sourced from its knowledge base. - Generates responses that are outside of its designated domain expertise. - Includes incorrect information despite referencing valid sources. - Delivers excessively long messages, which is particularly problematic for mobile users. |
| Action Execution | The agent fails when attempting to perform a specific function or task. | - Invokes the wrong actions or unexpected actions. - Returns error messages instead of completing the requested action. - Unnecessarily suggests escalating to a human agent. - Fails to properly collect the required input variables from the user. |
| Guardrails & Instructions | The agent violates predefined rules, constraints, or conversational boundaries. | - Disregards explicit operational instructions. - Makes unexpected or premature escalation attempts to human agents. - Shows inappropriate "Please Hold" messages during action execution. - Displays generic error messages like "Can't Help With That Right Now" or "System Error." |
| Knowledge Retrieval | The agent has problems sourcing and presenting information from its knowledge base. | - Retrieves irrelevant articles from the knowledge base. - Includes unnecessary or unwanted information in its responses. |
| Structured Guidance | The agent struggles to guide users through multi-step processes. | - Provides generic, ungrounded troubleshooting advice. - Presents too many steps within a single message. - Loses context during an ongoing troubleshooting process. - Gets stuck on individual troubleshooting steps. - Repeats questions despite having already received valid responses. |

##### Best Practices for Testing AI Agents

The following outlines best practices to keep in mind when testing Agents on Agentforce.

1. **Enhance Test Data**  
	The foundation of effective testing is comprehensive and realistic test data. Follow these principles to ensure that you have effective test data for testing your agents:
	- **Sufficient Coverage**: Aim to have enough test data to cover all critical topics and user personas.
		- **Realistic Scenarios**: Ensure that your test data accurately represents real-world user interactions.
		- **Negative and Edge Cases**: Include negative test cases (what the agent should *not* do) and edge scenarios to challenge the agent's boundaries.
		- **Guardrails Testing**: Add specific test cases designed to verify that the agent's guardrails are functioning correctly.
2. **Optimize Test Runs**  
	To make the most of your testing resources, optimize how you run your tests. The following are considerations when testing Agentforce agents:
	- **Test Case Volume**: You can utilize up to 1,000 test cases.
		- **Run Concurrent Tests**: It's possible to run up to 10 test cases at once within a 10-hour time period.
		- **Manage Resources**: Be mindful that running tests consumes credits. Ensure you are satisfied with your test data before initiating a run to avoid unnecessary costs.
3. **Review Results**  
	Carefully analyze test outcomes to identify areas of improvement:
	- **Analyze Failures**: Inspect each failed test case individually. Carefully read and understand the difference between the expected and the actual results to pinpoint the issue.
		- **Use a Sandbox Environment**: Testing agents can modify CRM data. *To prevent unintended changes to your live data, always conduct testing in a non-production environment, like a sandbox or a scratch org.*
4. **Tune and Retest**  
	Testing is an iterative process that continues as the agent evolves:
	- **Test Continuously**: Perform testing after every modification to the agent's topics or actions. This validates the changes and ensures that quality is maintained.
		- **Expand Test Coverage**: Continuously curate and expand your dataset with new test cases to improve the overall coverage and robustness of the agent.

##### Testing Approaches

Given the agent's complexity, no single testing method is sufficient. A comprehensive validation strategy must be layered, combining different approaches to cover everything from predictable, deterministic actions to the nuances of its non-deterministic, conversational behavior. These approaches provide a framework for systematically evaluating every component of the agent to ensure that it is robust, reliable, and secure.

1. **Manual Testing with Agent Simulator and Plan Tracer**
	- **Purpose**: This is the initial and often simplest way to test an agent. It's ideal for a small set of sample use cases and for gaining a foundational understanding of the agent's behavior.
		- **Mechanism**: An agent simulator provides a controlled environment where developers and administrators can directly interact with the agent. This simulator allows for detailed tracing of the information being provided by the admin/developer, offering insights into how the agent processes inputs and generates outputs.
		- **Benefits**:
		- Quick feedback
				- Easy to identify immediate issues
				- Helps in understanding the agent's logic flow
2. **Automated Testing with Testing Center or AFDX Test Suite**
	- **Purpose**: Once manual testing has established a baseline of functionality, automated testing becomes crucial for scalability, thoroughness, and regression testing.
		- **Mechanism**: Tools like the Testing Center or the AFDX test suite enable the generation of automated tests based on predefined sample use cases. These tests are designed to validate whether the agent's instructions and sub-agent classifications are working correctly across a broader range of scenarios.
		- **Benefits**:
		- Ensures consistent performance
				- Identifies subtle bugs
				- Supports continuous integration/continuous deployment (CI/CD) pipelines
				- Provides comprehensive coverage
3. **Action-Specific Unit Testing using Apex and Flows**
	- **Purpose**: To validate the deterministic business logic encapsulated within agent actions. While the agent's overall behavior is non-deterministic, agent actions are often powered by technologies like Flows and Apex, to which standard development practices apply.
		- **Mechanism**: Developers write unit tests for the specific Flows or Apex classes that an agent action invokes. These tests verify the individual components of the agent's logic, ensuring they produce the expected outputs for a given set of inputs.
		- **Benefits**:
		- Integrating these unit tests into a DevOps pipeline provides an automated safety net
				- Validates that any changes or enhancements to an action's logic do not introduce regressions
				- Ensures the reliability of the agent's capabilities before they are deployed to production
4. **Adversarial Testing - Security and Guardrail Enforcement**:
	- **Purpose**: Building various kinds of agents necessitates a strong emphasis on security and ensuring they operate within defined parameters and guardrails. This is paramount to preventing unintended actions, data breaches, or misuse. Therefore, the purpose of adversarial testing is to proactively identify and remedy these potential vulnerabilities by deliberately challenging the agent with inputs designed to circumvent its safety mechanisms, thereby testing its robustness and resistance to manipulation.
		- **Mechanism**: Adversarial testing is implemented by crafting challenging, ambiguous, or malicious inputs that push the boundaries of the agent's intended behavior. While platform tools like the "Guardrails" feature in Agent Builder provide insights into instruction adherence, developers should also create custom adversarial test cases that actively attempt to make the agent fail in a controlled environment.
		- **Benefits**: This approach systematically mitigates security and compliance risks before deployment. By identifying potential failure points, adversarial testing enhances agent trustworthiness and ensures it will operate securely and as intended when interacting with users.

##### Iterative Testing in Scratch Orgs and Sandboxes

The “inner loop” is the critical, iterative cycle where an agent moves from concept to a validated component, ready for deployment. This process of continuous refinement requires environments for both development and testing. Agentforce provides this framework through scratch orgs, which are isolated, temporary environments for rapid prototyping that doesn’t impact shared environments, and Sandboxes, which enable thorough testing with realistic data to accelerate the path to production.

1. **Development in Scratch Orgs**: Initial development should occur in a scratch org. The tools provided within the development environment, like Agent Builder and AFDX, are fully utilized here. Scratch orgs are strong candidates for CI/CD pipelines to run unit tests, perform code analysis, and promote changes to higher environments.
2. **Deployment to Sandbox for Real Data Testing**: Once the agent’s core functionalities are developed in a scratch org, deploy to a sandbox. Sandboxes are copies of a production environment, offering a more realistic testing ground.
	- **Real Data vs. Mock Data**: While some developers might mock data in scratch orgs for initial testing, deploying to a sandbox allows for testing with "real data." This is critical for evaluating the agent's performance in scenarios that closely mirror actual customer interactions. Using more representative data in a sandbox significantly accelerates the development and refinement process.
		- **Full or Partial Sandbox for Core CRM Data**: Depending on the data volume and specific testing requirements, either a full or partial sandbox can be utilized.
		- **Full Sandbox**: Provides a complete replica of the production environment, including all metadata and data. Ideal for extensive testing and performance tuning with large datasets.
				- **Partial Sandbox**: Contains a subset of the production data, often sufficient for testing specific features or functionalities where a full dataset is not strictly necessary.
		- **Knowledge and RAG Management**: If the agent relies on a knowledge base or Retrieval-Augmented Generation (RAG) model, ingest all relevant content into the sandbox and re‑index. This ensures that the agent uses current information during testing and can accurately retrieve and synthesize content.

Agentforce defines agents through metadata, so they can be deployed using standard Salesforce procedures like Change Sets or AFDX. This phase emphasizes a safe and controlled rollout through critical features like agent versioning and a separate activation step, which ensures system stability and allows for rapid recovery from issues.

Follow these steps to deploy and release your new agent.

1. **Deploy via Change Set/Metadata API or AFDX**: The deployment process for agents leverages standard Salesforce procedures, treating agents as metadata. This should be a familiar process for anyone accustomed to Salesforce development and deployment. Utilizing change sets or AFDX ensures a structured and consistent approach to migrating agent configurations between environments, such as from sandbox to production. This method facilitates version control and proper change management, which are crucial for maintaining system stability and reliability.
2. **Activate Agents Post-Deployment**: Following a successful deployment, it is imperative for a system administrator to actively "activate" the agent. Deployment simply places the agent's code and metadata into the target environment; activation is the step that makes the agent operational and available for use. This separation allows for controlled rollout and testing before an agent becomes live and interacts with end-users or other system components.
3. **Use Versioning for Safe Agent Management**: Agent versioning is a critical feature that significantly enhances the safety and flexibility of agent development and maintenance.
	1. **Creating, Testing, and Publishing New Versions**: The recommended practice involves creating a new version of an agent whenever changes or enhancements are required. This new version can then be thoroughly tested in a sandbox environment without impacting the live, activated agent. Once the new version has been validated and is deemed ready, it can be published and subsequently activated, replacing the previous operational version. This iterative process allows for continuous improvement and innovation while minimizing disruption.
		2. **Rollback to Previous Versions**: A key benefit of versioning is the ability to quickly and easily revert to a previous, stable version if an issue arises with a newly deployed or activated agent. If something goes wrong—for example, if an agent misbehaves or introduces an unforeseen error—administrators can simply roll back to the last known good version and activate it. This capability provides a critical safety net, allowing for rapid recovery and minimizing downtime, thereby ensuring business continuity and user satisfaction.

##### Agent Monitoring

Agentforce Session Tracing is an open, extensible model built on Data 360 that captures end‑to‑end agent interactions. Agentforce session tracing ingests data from different sources (starting with reasoning engine logs) and combines everything under a session ID.

The Session Tracing Data Model (STDM) provides detailed information into what happened during agent sessions, including:

- Turn-by-turn interactions
- Reasoning engine executions
- Actions, prompt and gateway inputs/outputs
- Error messages
- Final responses

The STDM is a critical tool to help developers:

- Debug agent setup and configuration issues during build time.
- Learn why certain test cases failed during batch testing.
- Address why an agent isn’t able to handle a set of user questions or is going off-topic.

Developers should use this session trace data to observe, monitor, investigate, and troubleshoot agent events, incidents, and behavior patterns.

The STDM comprises Data Lake Objects (DLOs) and Data Model Objects (DMOs) that store detailed logs of agent behavior. Metadata about each LLM call made by the reasoning engine can be joined with feedback or guardrails metrics. Data streams into DLOs in Data 360 and maps to applicable DMOs.

Developers can access this data and get insights by running queries and reports against the STDM. The components of an STDM are described below.

**Agentforce Session Tracing Data Model ERD**

![An entity relationship diagram showing the entities and relationships of the Agentforce Session Tracing Data Model](https://a.sfdcstatic.com/developer-website/prod/images/architect/agentforce-session-tracing-data-model-erd.png)

| Data Lake Object/Data Model Object | Description |
| --- | --- |
| AIAgentSession | An overarching container capturing contiguous interactions with one or more AI agents. |
| AIAgentSessionParticipant | An entity (human or AI) that takes part in an AIAgentSession. |
| AIAgentInteraction | A segment within a session. It typically begins with a user's request and ends when the AI agent provides a response to that request. |
| AIAgentInteractionStep | A discrete action or operation performed during an interaction to fulfill the user's request. |
| AIAgentInteractionMessage | A single communication provided by the user or generated by the AI agent during a session. |

##### Agentforce Optimization

Agentforce Optimization is a powerful feature designed to enhance the performance of AI agents by providing in-depth insights into user interactions. Built upon the analytics capabilities of the Session Tracing Data Model (STDM), it allows administrators and developers to understand user topics, engagement patterns, and the effectiveness of agent resolutions.

Key aspects of Agentforce optimization include:

- **Moment-Specific Data**: Agentforce Optimization extends STDM by introducing "Moments," which represent interactions focused on a specific user intent or request during a session. This granular data allows for detailed inspection of every aspect of an interaction, from the initial user request to the agent's resolution.
- **Automated Moment Processing**: Moments are generated daily, and then clustered and tagged weekly across all active agents using an advanced Large Language Model (LLM). This segmentation simplifies querying and provides insights into various facets of agent sessions.
- **Querying and Analysis**: Users can query Moments based on tags, quality scores, and other criteria. This enables the assessment of user engagement through metrics like Moment duration and relevance quality scores, helping pinpoint areas for improvement.
- **Unified Data Model**: Agentforce optimization leverages the unified Session Tracing Data Model (STDM), which captures every logged event within a session, including individual conversation turns. All relevant entities are provisioned upon enabling STDM in the setup.

By analyzing AI agent interactions, Agentforce optimization empowers users to identify areas for improvement and refine configurations to better meet user needs.

For more information, see [Data Model for Agentforce Optimization](https://help.salesforce.com/s/articleView?id=ai.generative_ai_optimize_data_model.htm&type=5).

This chapter is a practical guide for pro‑code developers. It shows how to build, test, and deploy agents with Agentforce DX (AFDX) and our Python SDK with speed and safety. We will walk through the entire lifecycle, from initial design to a version-controlled agent, using the powerful combination of AFDX and our Python SDK.

The following examples will leverage two key toolsets designed for building and managing agents on the Agentforce platform. A foundational understanding of these tools is recommended to get the most out of this guide.

**1\. Agentforce DX (AFDX): For Managing the Lifecycle**

Agentforce DX extends the familiar Salesforce Developer Experience (SFDX) toolset—including the Salesforce CLI and VS Code extensions—to support the entire Agent Development Lifecycle. It is used to manage an agent as version-controlled metadata, automate testing from the command line, and orchestrate deployments between your development sandboxes and production.

To learn more, see: [Getting Started with Agentforce DX Development](https://trailhead.salesforce.com/content/learn/projects/create-an-agent-using-pro-code-tools/get-started-with-agentforce-dx).

**2\. Agentforce Python SDK: For Building the Agent**

The Python SDK provides the programmatic interface for the "inner loop" of development. It allows you to define an agent's reasoning logic, connect its tools, and manage prompt templates directly within a familiar Python environment, streamlining the core construction phase of the ADLC.

The SDK is available on PyPI: [https://pypi.org/project/agentforce-sdk/](https://pypi.org/project/agentforce-sdk/).

The complete project is available here:  
[https://github.com/akshatasawant9699/ADLC\_Whitepaper](https://github.com/akshatasawant9699/ADLC_Whitepaper).

This foundational phase defines the purpose, persona, and core capabilities of an agent. It involves answering critical questions to architect the agent's "brain" before any code is written. In this example, we're designing an agent for *Coral Cloud Resorts*.

- **Mission**: The agent acts as a resort manager, handling customer complaints, managing employee schedules, and ensuring smooth resort operation.
- **Persona**: The agent has a helpful, professional, and conversational tone.
- **Tools and Capabilities**: The agent needs access to reservation systems, employee scheduling software, and resort policies.
- **Decision Logic**: The agent uses AI-generated topics to determine user intent and generate appropriate actions.

With *Agentforce DX*, the design phase translates into a tangible specification file: [**Agentforce DX: Generating an Agent Specification**](https://developer.salesforce.com/docs/einstein/genai/guide/agent-dx-generate-agent-spec.html). The first step in the pro-code journey is to generate an **agentSpec.yaml** file. The YAML file captures the agent's core design, including its role, relevant company details, and an AI-generated list of topics that define the jobs that it can handle.

Use the Salesforce CLI to generate this spec via interactive prompts. To begin creating your agent with Agentforce DX, run:

You’ll need to provide specific details that were defined during the ideation phase:

- **Type of agent**: Customer
- **Company Name**: Coral Cloud Resorts
- **Company Description**: Coral Cloud Resorts provides customers with exceptional destination activities, unforgettable experiences, and reservation services, all backed by a commitment to provide top-notch customer service.
- **Agent Role**: The resort manager fields customer complaints, manages employee schedules, and ensures that all processes are running smoothly.

Running this command creates an **agentSpec.yaml** file in the DX project's *specs* directory. The file contains the information that was provided along with a list of AI-generated topics that include the name and description of each topic. Review and edit the file as needed to refine the agent's capabilities.

Similarly, the Python SDK implementation uses interactive specification collection to auto-generate agent topics with proper scope fields required for SDK compatibility.  
Further, it’ll create a complete agent specification JSON file which will be used to create an agent in Phase 2.

The development phase focuses on constructing the agent's core components: the reasoning engine, tools it can use, and its knowledge base. *Agentforce* abstracts much of the complexity, which allows developers to focus on business logic.

This section shares two pro-code approaches for the Agentforce development phase. Firstly, using the Agentforce DX and secondly using Python.

##### Agentforce DX: Create an Agent from a Specification

Once the **agentSpec.yaml** file is ready, create the agent in your Salesforce org. Run this command to create the agent and sync its associated metadata back to your local DX project:

When prompted, accept the default API name, **Resort\_Manager**. The command parses the spec, creates the agent, and retrieves the metadata. The metadata includes a **Bot**, **BotVersion**, and a **GenAiPlannerBundle**, which add AI intelligence and references to the agent's topics and actions.

Preview the agent's structure before creating it by adding the **\--preview** flag to generate a local JSON file that details the type of agent that the LLM *will* create, including suggested actions. For example:

**For more information refer to [Create an Agent from Your DX Project](https://trailhead.salesforce.com/content/learn/projects/create-an-agent-using-pro-code-tools/create-an-agent-from-your-dx-project) from Trailhead.**

##### Agentforce Python SDK: Define Specific Tools

The Agent SDK facilitates agent testing by creating mock actions. These mock actions will eventually need to be replaced with real actions within Salesforce. Salesforce offers a range of platform features, including Flows, Apex, Prompt Templates, and APIs, all of which can be encapsulated as Agentforce actions.

Here's a mocked action code snippet to illustrate how an Agentforce action might look.

*The implementation establishes the connection to Salesforce, creates the agent instance, and defines custom tools and actions that the agent can use to interact with external systems and perform specific business functions.*

As we have discussed above, testing an agent is more complex than traditional software testing. It requires validating behavior, reasoning, and robustness across various scenarios. This includes unit testing for individual tools, end-to-end testing for conversations, and adversarial testing to find vulnerabilities.

*Agentforce DX* provides a high-level workflow for creating, deploying, and running tests in addition to the Testing Center and the direct Testing API. This section demonstrates executing tests with Agentforce DX.

##### Agentforce DX: Run an Agent Test

Use *Agentforce DX* to run predefined agent tests directly from the command line. This is ideal for integrating agent testing into modern DevOps processes.

##### Agentforce Python SDK: Simulate E2E and Adversarial Tests

Conceptually, *Python SDK* allows for scripted conversations to simulate end-to-end (E2E) tests and validate agent reasoning.

##### Agentforce Python SDK with Salesforce Testing API

The Python SDK implementation uses comprehensive testing with Salesforce Testing API and AiEvaluationDefinition metadata, creating structured test cases with expectations for topic sequences, action sequences, string matching, and quality metrics. The system generates XML metadata definitions that can be deployed to Salesforce for automated agent testing and validation.

Once validated, the agent deploys into a production environment. During this phase, *Agentforce DX* is crucial in helping to manage and move agent metadata between different orgs (for example, sandboxes and production). Agent deployments create a new version of the Agent and the Agent doesn't go live until you explicitly activate it. This gives you full control of when to release the new version of the agent.

##### Agentforce DX: Deploy Agent Metadata

The standard *Salesforce DX* project structure organizes agent metadata under the **force-app** directory. Use standard **sf project deploy** commands to deploy an agent and its associated tests to a target org.

After an agent is created or deployed, you can open it directly in the *Agentforce Builder UI* to verify its configuration by running:

After you validate that the agent is deployed, you can activate it. If you encounter any unexpected issues, roll back to the previous working version of the agent.

##### Agentforce Python SDK: Deploying Agent Deployment

The implementation takes the validated agent specification and deploys it to the Salesforce org, making the agent available for use. The deployment process includes agent creation, metadata synchronization, and verification of successful deployment.

ADLC is a continuous cycle; deployment isn't the end. Agents are living systems that require constant monitoring to track metrics like latency, cost, and success rates. The insights gained from monitoring are used to tune and improve agent performance through prompt engineering, tool optimization, and refining knowledge bases.

The *Agentforce* platform provides comprehensive dashboards and analytics to support this crucial phase, ensuring that agents continue to evolve and improve over time.

##### Agentforce Analytics

Agentforce Analytics, found in the Agentforce (Default) folder, uses Data 360 to provide insights into agent performance. The customizable dashboard and reports offer data on adoption, feedback, and usage, helping you refine topics and actions to improve user satisfaction. You can drill down into results by clicking charts or linked reports. To customize, clone existing reports and modify the clones to avoid disrupting analytics processes.

![Agentforce Analytics Dashboard](https://a.sfdcstatic.com/developer-website/prod/images/architect/agentforce-analytics-dashboard.png)

##### Utterance Analysis

Utterance Analysis shows how Agentforce (Default) users are using agents, what they're requesting, and whether the agent was able to handle these requests. These customizable reports can help you refine your topics and actions so that your agents respond more effectively and accurately.

![Agentforce Utterance Analysis Dashboard](https://a.sfdcstatic.com/developer-website/prod/images/architect/agentforce-utterance-analysis-dashboard.png)

##### Agentforce Python SDK: Monitoring with Data 360 Integrations

The Agent SDK implementation uses advanced monitoring and analytics with Data 360 Python Connector, establishing connection to Salesforce Data 360, querying agent performance metrics, and creating comprehensive monitoring dashboards.  
The system tracks response times, success rates, user satisfaction, and cost metrics to provide actionable insights for agent optimization.

##### Agentforce DX: Agent Monitoring

The implementation uses standard AFDX commands with CLI-based agent management, keeping the agent up-to-date with platform changes and incorporating user feedback for continuous improvement.

Refer the GitHub repository [here](https://github.com/akshatasawant9699/ADLC_Whitepaper) for ADLC implementation using Agent SDK and AFDX.

Mastering the Agent Development Lifecycle requires adhering to a set of core principles that ensure efficiency, reliability, and strategic alignment. The following guidelines synthesize the key lessons from each phase of the ADLC into a strategic framework for architects and developers.

**1\. Planning and Ideating**

This initial phase focuses on aligning the agent's purpose with business goals and ensuring it is built on a solid foundation.

- **Prioritize for Business Impact**: Begin by mapping potential use cases directly to strategic business goals. Use a prioritization matrix to score their potential impact and start with a single, focused use case with clear KPIs.
- **Involve stakeholders early**: Gather insights on pain points and ensure alignment.
- **Leverage Data Insights**: An agent is only as good as its data. Use Data 360 to explore available structured and unstructured data to inform the agent's context and capabilities. Review existing reports and dashboards to identify current trends that can inform your use case selection.
- **Use Frameworks for Ideation**: Apply structured ideation methods to brainstorm and refine potential applications, such as design thinking or SWOT analysis.

**2\. Building Agents**

This phase covers the best practices for constructing a high-performing and efficient agent.

- **Avoid Too Many Topics**: Limit the number of topics to reduce the risk of creating similar or overlapping topics that could confuse the agent.
- **Keep Instructions and Prompts Concise**: Use direct, simple language and provide example utterances to guide the agent effectively.
- **Leverage Variables and Deterministic Actions**: Use these tools to guide the agent's behavior and optimize its performance for more predictable outcomes.
- **Keep Action Outputs Small and Concise**: Ensure the agent's responses are brief and to the point. Longer outputs use more context and are slower to generate.
- **Optimize Actions for Speed**: Design Flows and Apex classes to return minimal required data. Aim to have fewer actions needed to generate a response by pre-processing where possible.
- **Define a Clear Scope**: Write proper descriptions, instructions, and scope for actions to prevent the agent from calling RAG (Retrieval-Augmented Generation) for out-of-scope questions.
- **Use Hybrid Search Sparingly**: Only use hybrid search if it is absolutely necessary, as it can negatively impact latency.

**3\. Testing, Monitoring, and Tuning**

This iterative phase is crucial for refining the agent's accuracy and performance.

- **Establish a Testing Flow**: Follow a consistent testing cycle:
	1. **Run Batch Test**: Execute a comprehensive set of tests.
		2. **View Scores/Errors**: Analyze the performance metrics and identify failures.
		3. **Inspect Failures**: Examine each failure row to understand the discrepancy.
		4. **Update Agent**: Make the necessary adjustments to the agent or its evaluation data.
- **Review Session Tracing Information**: Use the Session Trace Data Model and Agentforce Interaction Explorer to perform root cause analysis when issues or unexpected behaviors are identified. Tune your agent based on the information and continue iterating your agent.

The *Agent Development Lifecycle* represents a critical evolution of traditional software development principles, designed for the era of intelligent, autonomous systems.

- **Evolution, Not Replacement**: Agent Development Lifecycle extends and enhances traditional Application Lifecycle Management without replacing it.
- **Data as a First-Class Citizen**: Data plays a far more dynamic and central role in agent development.
- **Specialized Tooling & Skills**: Requires new tools and a broader set of specialized skills across data science, ML engineering, and agent development.
- **Continuous Learning**: Agent development adds continuous *learning* and *adaptation* of the system itself.
- **Future Impact**: Agentic AI promises to further automate and optimize complex IT operations and software development workflows.