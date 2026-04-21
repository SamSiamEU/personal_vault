Over two decades ago, Salesforce pioneered the first multitenant cloud platform, setting a precedent in the industry. Since then, Salesforce has evolved into a comprehensive enterprise platform, capable of encapsulating and automating key aspects of a business, and serving hundreds of thousands of businesses and millions of users in various industries and regions. Salesforce has also enhanced its Customer360 product suite through strategic acquisitions.

Over the last several years, shifts in the market, the industry, and the technology landscape have led us to a number of deep transformations in the foundational Salesforce Platform. These include:

- The emergence of public cloud providers who invest heavily in infrastructure.
- Rapid advancements in AI, including machine learning, generative AI, and agentic experiences.
- Increased data residency and regulatory requirements across industries and countries.
- The need for handling real-time data and transactions at a rapidly increasing scale.
- Increased focus on requirements for cybersecurity, system availability, performance, and resilience.
- Customer demand for an integrated suite that offers a highly resilient, loosely coupled, and strongly coherent architecture.

In response to these changes, particularly the seismic shift of AI and its impact on businesses, Salesforce has completely transformed its platform from the ground up, laying the groundwork for the next generation of applications and customer use cases, all while upholding our trust goals.

The launch of Agentforce at Dreamforce 2024 and the diagram below represents the culmination of this extensive effort, involving thousands of Salesforce Technology and Product organization team members. Currently, more than 95% of our customers have transitioned to this new platform. The successful migration of a majority of our customers, including those with the most demanding workloads, underscores the ingenuity of our engineers and reaffirms Salesforce’s core values of Trust, Customer Success, and Innovation.

Since the launch of Agentforce, Salesforce has continued to pioneer the use of AI in enterprise applications and has been a market leader in developing agentic experiences that provide real-time, conversational experiences for existing and new business capabilities.

In this white paper, crafted in collaboration with top engineers, a detailed exploration is provided for builders who appreciate the complexities behind major technological transformations. The paper delves into the essential architectural enhancements that keep the platform scalable, secure, and ready to handle future applications while meeting the changing needs of our customers. It’s recommended that you begin with the Architecture Overview chapter to understand the full picture. From there, readers can either continue in sequence or explore the chapters that capture their interest the most.

*Emin Gerba*  
*Chief Architect, Salesforce*

![Platform Architecture Overview](https://a.sfdcstatic.com/developer-website/prod/images/architect/platform-architecture-overview.png)

The architectural principles of the Salesforce Platform below capture the foundation and differentiation for how we engineer features and capabilities:

- **Enterprise-Grade Trust**: Trust is Salesforce's #1 value, and we prioritize not only the availability and security of our services, but also build the access control, compliance and security features so our customers can meet their compliance and security standards with the Salesforce Platform.
- **Multitenant**: All services and infrastructure are built to host multiple customers. This provides a strategic pattern for scaling with use, as well as standardizing on a common high-bar of availability and security regardless of the size of our customers.
- **Metadata-Driven**: Metadata is at the heart of how our multitenant services are customizable. Our metadata is extensible so that admins and developers can build upon ‌existing work, as well as benefit from future product updates from Salesforce and ecosystem partners.
- **API First:** The Salesforce Platform prioritizes a rich and coherent API portfolio that covers everything that can be done via Salesforce-native user interfaces. This allows developers and partners to leverage and re-compose the platform’s functionality for integrating systems or building new user experiences.
- **Open and Interoperable**: The Salesforce Platform can be integrated into any of our customers’ enterprise architectures. We designed the Salesforce Platform to work with other cloud-based and on-prem systems, as well as provide APIs, tools, and integration standards for external systems to integrate with the Salesforce Platform.
- **Agentic:** The Salesforce Platform is rapidly evolving to be agent-first across the entire application suite. We want users to be able to engage with Salesforce through deep agentic conversational experiences that allow them to get work done and interact with their data in increasingly natural ways.

The current Salesforce Platform represents the latest stage in the evolution of Salesforce’s capabilities since the 2008 debut of the Force.com Platform. Recent key transformations include:

- Adoption of Hyperforce and a shift to cloud-based architectures.
- Evolution from a monolithic architecture to a structure with independent services.
- Introduction of Data 360 and Lakehouse technologies alongside traditional relational data stores.
- Deep integration of AI technologies, generative and machine learning, and an evolution to agentic experiences across the platform.

These changes have expanded and refined the platform’s capabilities without significant disruptions, thanks to robust abstractions that allow Salesforce engineers to advance our technologies seamlessly with minimal customer disruption. The robust abstraction also continues to be key to the Salesforce Platform’s value of simplifying the technical complexities of enterprise-grade software, like security, availability, and technology conventions, so app developers can focus on solving their unique challenges. The Salesforce Platform’s capabilities are highlighted below:

![Next Gen Platform Architecture Overview](https://architect.salesforce.com/ns-assets/legacy/image2-architectureoverview.png)

The Salesforce Platform is shown as a set of layers that make up the system. Each layer represents a group of related features that are important to applications built on the platform. The sub-boxes within each layer provide illustrative examples of these capabilities. Each lower layer’s capabilities are integrated into all the layers above, ensuring a consistent and coherent experience across the entire Salesforce application suite.

The Salesforce Platform embodies extensive engineering transformations across all layers of a mature technology platform developed over the past 20 years. Driven by evolving customer demands and new technologies, these changes enable support for new app types and solutions. The transformations are interconnected, with changes in lower layers influencing the evolution of all subsequent layers above.

The Salesforce Platform is structured into several layers, each contributing to its comprehensive capabilities:

- **Hyperforce**: The foundational infrastructure has evolved from first-party data centers to public cloud providers, enhanced with Salesforce technologies for secure, compliant, highly-available, and cost-efficient hosting.
- **Metadata Framework**: Provides a stable abstraction for apps to build on, even as the technologies we have and use evolve. Includes an object-relational mapper, prescriptive order of execution, and a “core” runtime that bridges the metadata definitions with the metadata-driven runtimes.
- **Data**: Includes a multitenant relational database and a petabyte-scale Lakehouse for managing Salesforce and non-Salesforce data, supporting unstructured data and content management, advanced search, governance, and analytical processing capabilities.
- **AI**: Builds on the data layer with foundational, trusted AI technologies that leverage predictive and generative AI to power agentic experiences.
- **App Platform Services:** Provides tools for IT admins, developers, and vendors to build and customize applications, offering an opinionated abstraction to simplify common and complex tasks.
- **Business Capabilities**: Offers a range of capabilities to meet diverse business needs, allowing developers to tailor applications as needed.
- **APIs and API Management**: Ensures all platform capabilities are accessible through well-formed APIs, facilitating service and layer interdependencies.
- **User and Developer Experience**: Features user-friendly interfaces for end-users and a range of development tools from low-code to pro-code for application development and customization, with support for modern AI-driven development.
- **Integration**: Integrates with any enterprise architecture, enabling compatibility with Salesforce and non-Salesforce systems through data connectors, zero-copy data integration and other tools.
- **Apps and Industries**: Provides a suite of customizable apps and industry-specific solutions built on the platform’s integrated capabilities, leveraging the full range of lower-layer functionalities, and with deeply integrated AI agents.

Salesforce has been developing global data center infrastructure for nearly 25 years, predating many current hyperscalers and IaaS vendors. Hyperforce, the current generation of Salesforce’s infrastructure evolution, is designed to operate across multiple public cloud providers worldwide.

It’s tailored to meet customer needs for elastic B2C scale, global data residency, enhanced availability, top-tier security, and regulatory compliance. Hyperforce standardizes infrastructure across all Salesforce products, facilitating rapid integration of new acquisitions.

Hyperforce ensures delivery of the Salesforce Platform, allowing for swift deployment of new features and applications, meeting data residency and regulatory compliance requirements in more than 20 regions across the world.

During Salesforce’s transition to Hyperforce, significant differences in services, interfaces, and compliance levels among hyperscalers were identified. To build a robust and portable foundation for the Salesforce Platform, these architectural principles were adopted:

- **Infrastructure as Code**: Utilizing a domain-driven architecture, this principle involves declarative coding for infrastructure, creating immutable artifacts, and automating infrastructure on-demand using standards like Kubernetes and Service Mesh.
- **Zero-Trust Security**: Implementing a zero-trust security model with comprehensive defense strategies including identity management, authentication, authorization, network isolation, least privilege security policies, and encryption of data both in transit and at rest.
- **Managed Services**: Emphasizing the use of multitenant and multi-cloud services, this principle enhances portability across different infrastructures and environments such as commercial, government, and air-gapped systems.
- **Built-in Resilience**: Mission-critical services are spread across multiple Availability Zones to ensure high availability. Data is replicated across Availability regions. Services are also labeled with availability tiering to manage service level objectives and resilience planning.
- **Fully Observable**: Integration of all services into a standard observability platform for efficient monitoring, which includes log collection, metrics gathering, alerting, distributed tracing, and tracking of service operations like traffic volume, error rates, and resource utilization.
- **Automated Operations**: This includes automated management of infrastructure lifecycle and predictive AIOps (AI for operations) for maintaining quality of service, detecting, and addressing service degradations, and failure detection.
- **Automated Scale**: Focusing on scalability and cost-efficiency, this principle allows for operational flexibility across different scales without increasing operational risks, abstracting specific account limits related to the cloud provider.
- **FinOps Aware**: Public cloud brings infrastructure agility, but with the risk of elevated costs. We embrace an efficiency-driven engineering culture throughout the service lifecycle, without compromising on availability, security, and customer trust.

These principles guide the development and operation of Salesforce’s Hyperforce platform, ensuring it remains adaptable, secure, and efficient across various environments.

The Salesforce Platform and its supporting services run on the Hyperforce Foundation, which comprises multiple Hyperforce Instances. These instances are strategically distributed across various countries to align with customer preferences for geography and availability. To meet stringent data residency and operational requirements, one or more Hyperforce Instances can be optionally grouped and designated as an Operating Zone. Each instance is regularly updated to ensure safety, scalability, and compliance with local and legal standards.

Hyperforce Instances are made up of several Hyperforce Functional Domain instances, which are clusters of services delivering specific functionalities. Foundational functional domains provide critical services like security, authentication, logging, and monitoring, all of which are essential for other Hyperforce services. Business functional domains support various Salesforce products such as Sales Cloud, Service Cloud, and others, facilitating their product functionality.

Services within a Functional Domain may be organized into Cells, which are scalable and repeatable units of service delivery. The Hyperforce Cell corresponds to what is traditionally known as a "Salesforce instance" wherein one or more Salesforce organizations (org) reside. A cell is a scale unit as well as a strong blast radius boundary. Supercells provide a logical grouping of multiple cells to demarcate a larger blast radius due to shared services across cells. Multiple Supercells may be present in a Functional Domain. Cells and Supercells allow Hyperforce to scale horizontally within a functional domain while also maintaining strong control over the size of the blast radius.

Each Hyperforce Instance is mapped to one Availability Region, a concept found in all public cloud infrastructures, and is capable of operating independently of all other Hyperforce Instances. All mission-critical services and data in the Hyperforce Instance are distributed and replicated across at least three Availability Zones, to achieve ‌fault tolerance and stability. Furthermore, data backups are copied to other suitable Hyperforce Instances for business continuity and regulatory compliance.

Hyperforce infrastructure is continually evolving, as new Hyperforce Instances and Cells are created or refreshed in place. Customers are insulated from changes in the physical details of Hyperforce. All externally visible customer endpoints are accessed via stable and secure Salesforce My Domains (for example, acme.my.salesforce.com) that securely route traffic to the current data and service location. Outbound traffic (e.g., Mail, Web callouts) are best implemented using secure mechanisms like Domain Keys Identified Mail (DKIM) and mTLS, to ensure that customers’ on-premise infrastructure isn’t hardcoding the physical detail of Salesforce infrastructure, such as IP addresses that can change over time.

![Platform Infrastructure Concepts](https://architect.salesforce.com/ns-assets/legacy/image4-infrastructureconcepts.png)

Hyperforce Functional Domains are designed with robust security measures. Each domain is secured at the perimeter and isolated, with services within a domain separated into dedicated accounts for added security. Communication between services is facilitated securely via Service Mesh or similar protocols. Traffic management is handled by ingress and egress gateways that inspect, route, and apply necessary controls like circuit breakers or rate limits to all incoming and outgoing traffic.

Services within a Hyperforce Functional Domain are grouped into Security Groups, with only those in the edge group exposed to the public internet. Runtime security policies enforce communication rules between different security groups, adhering to the principle of least privilege to ensure services have only the necessary access.

Each geographical region has a Hyperforce Edge Functional Domain that terminates transport layer security and employs programmable web application firewall policies to preemptively address threats. This ensures that only legitimate traffic reaches Hyperforce endpoints while maintaining a secure and efficient customer experience. Additionally, internal network links between Hyperforce Instances are tightly controlled, and all log data containing personally identifiable information is anonymized to comply with GDPR standards.

A Hyperforce grid comprises multiple Hyperforce Instances sharing the same control plane, that is designed to isolate sensitive workloads where appropriate. It ensures zero leakage of any customer or system data, platform metadata, or monitoring data across grids. The Control Plane consists of redundant Hyperforce Instances that host essential services for creating, managing, and monitoring customer-facing Hyperforce Instances.

Service and infrastructure code for all Hyperforce services is securely developed within a dedicated control plane functional domain, utilizing source code management, continuous integration, testing, and artifact building services. The generated code is scanned for threats and vulnerabilities before it is packaged into standardized, digitally signed containers and stored in image registries. Code deployment is handled by authorized pipelines in the Hyperforce Continuous Delivery system, with deployment privileges restricted to authorized teams and operators. An Airgapped Control Plane handles additional safeguards necessary in such environments.

Identity and Access Management (IAM) services enforce just-in-time approval to limit access duration and actions, while audit trails monitor all activity, feeding into real-time detection systems to identify and alert on any suspicious activities.

As Salesforce transitions its services to Hyperforce on public clouds from its first-party data centers, it’s crucial to revamp our budget creation, cost visualization, and resource optimization strategies.

Our cost management approach isn’t just about cutting costs; it’s a strategic process that differentiates between products aimed at growth versus those that are stable. It plans for consumption-based pricing and margins that uphold product availability, aligning with our core value of Trust. Public cloud accounts are organized hierarchically and linked to specific products and executives. Detailed service-level resource tagging, enriched with organizational metadata, helps pinpoint costs for individual microservices. Tools like Tableau and Slack, along with advanced forecasting tools, are employed to provide executives and teams with real-time data on costs, forecasts, and budget analyses, instilling confidence in ‌future financial planning.

To ensure optimal cost management, Salesforce employs a mix of Compute Savings Plans, Spot Capacity, and On-Demand Capacity Reservations (ODCR), guaranteeing the necessary capacity. These reservations are managed through advanced time-series forecasting and custom dashboards, allowing for human oversight and decision-making. Setting achievable goals on unit transactional cost reductions (the cost to process a defined volume of business transactions) is an effective strategy to drive improvements. The Hyperforce Unit Cost Explorer tool enables teams to analyze and manage unit cost trends, attributing costs to specific services, and identifying new improvement opportunities. The Salesforce Cloud Optimization Index, or “COIN” score, assesses services against a dynamic list of savings opportunities, motivating service teams to maintain optimal resource efficiency.

In our unwavering commitment to Sustainability, we actively pursue reductions in our carbon footprint, setting specific targets to decrease our unit Carbon to Serve, a measure of emissions relative to work performed.

Security and availability are crucial foundational aspects of our enterprise-grade platform, essential for maintaining customer trust. At Salesforce, these controls are integral to the Salesforce Platform, automatically enforced through shared services and software frameworks. This built-in approach ensures that individual systems benefit without requiring additional effort.

Managing and continuously enhancing this extensive array of security and availability controls across thousands of services and hundreds of teams presents a significant challenge. However, it’s crucial, as overlooking even a minor detail can result in a security breach or system outage.

Hyperforce is a secure and compliant infrastructure platform that supports the development and deployment of services with advanced security features. It offers strong access control, data encryption, and compliance with security standards. Salesforce adheres to over 40 security and compliance standards such as PCI/DSS, GDPR, HIPAA, FedRamp, and more.

Key security principles include Zero Trust Architecture (ZTA) and end-to-end encryption, ensuring the protection of customer data across all processing stages. Salesforce adheres to security standards and best practices from the secure software development lifecycle to production operations, as well as robust application-level security practices to mitigate potential threats.

The ZTA cybersecurity paradigm ensures that all users, devices, and service connections undergo authentication, authorization, and continuous validation, regardless of location. ZTA and Public Key Infrastructure (PKI) are essential for modern cybersecurity, establishing trust boundaries and secure communication without relying on perimeter security.

However, PKI deployments often overlook the importance of certificate revocation and governance over root certificate authorities. Salesforce’s implementation of certificate revocation is robust and scalable, supporting end-to-end PKI security.

Additionally, Hyperforce enforces ZTA through mutual transport layer security between services, using short-lived private keys and just-in-time access for users with role-based access control.

The Salesforce Platform ensures the protection of data in transit by using TLS with perfect forward secrecy cipher suites, which secures data as it travels across the network between user devices and Salesforce services, as well as within the Salesforce infrastructure domains.

For data at rest, the Salesforce Platform employs a key management system supported by hardware security modules. In its multitenant platform, each tenant is assigned a unique encryption key, preventing any crossover of keys between tenants.

The security of communication and encryption is heavily dependent on entropy for generating keys or random data. Recognizing the vulnerability of cryptographic protocols to attacks due to predictable key generation, the Salesforce Platform mitigates this risk by sourcing entropy from multiple origins for all key generation processes. We leverage the memory encryption feature available in various processors, enabled by a cloud service provider, to enhance protection against cold boot attacks.

Salesforce has a customized JDK to meet many compliance standards, such as Federal Information Processing Standard (FIPS), simplifying the process for developers and operators by eliminating the need for them to undertake compliance work themselves. This customization not only helps prevent risks such as XML external entity injection (XXE) but also enhances Salesforce’s cryptography agility and ability to interchange cryptography strategies as needed. It allows the transformation of non-compliant code—whether developed internally or sourced from open repositories—into FIPS-compliant code without necessitating a complete rewrite, thus reducing the workload on development teams and maintaining adherence to secure-by-default design principles.

Additionally, Salesforce has incorporated frameworks to counter vulnerabilities like cross-site scripting (XSS), request forgery (CSRF), and SQL injection by integrating protective measures into the Secure Software Development Lifecycle (SSDL).

A centralized secrets management system, reinforced by role-based access controls (RBAC), is implemented to secure both services and user access. Furthermore, code scanning tools are employed to prevent the accidental exposure of secrets in production environments through source code management systems.

Phishing remains a significant threat to organizations, leading Salesforce to implement phishing-resistant multi-factor authentication (MFA) in accordance with a number of industry best practices, including CISA (Cybersecurity and Infrastructure Security Agency) Zero Trust principles. This includes hardware-backed keys for employees with production access and a secure kernel for controlled access to cloud service provider accounts.

To maintain a robust security posture, Salesforce has standardized security controls and integrated cloud-native security services into Hyperforce, providing enhanced visibility, threat detection, and policy enforcement. A comprehensive security information and event management system is in place for real-time monitoring, alerting, and reporting, which is supported by a thorough vulnerability management program and cloud security posture management tools to continuously identify, assess, and remediate vulnerabilities.

Additionally, a web application firewall filters and monitors HTTP traffic to protect against various attacks, and a range of network security tools including firewalls, intrusion detection and prevention systems, virtual private networks, and endpoint detection and response agents are utilized to provide continuous monitoring and threat detection. Network segmentation and micro-segmentation are implemented to minimize the attack surface and contain potential breaches.

Salesforce has also developed and implemented a robust incident response plan tailored to the unique challenges of Hyperforce, featuring predefined procedures for identifying, containing, and mitigating security incidents, ensuring a rapid and effective response to potential security threats.

Salesforce manages mission-critical customer workloads that demand high availability. Our strategy for high availability includes various organizational facets such as our service ownership model, incident management, and operational reviews. Key technical elements of our strategy include our monitoring architecture, AI-driven operations automation, and automated safety mechanisms for production changes.

To consistently achieve high availability across thousands of services, a three-step approach manages technical risks at scale.

First, availability architecture standards are established, defining best practices such as:

- **Redundancy with automated failover**. To handle the constant failures that a large cloud-based system encounters, Salesforce builds its services with a high level of redundancy, fully automated failure detection, and seamless automated recovery for both complete and partial failures.
- **Limit blast radius**. Failures *will* happen, and so the team designs all of its services with intentional blast radius maximums to cap the impact of failures. The most classic and visible example is that of the Hyperforce Cell (fka Pod).
- **Compartmentalize failures**. Prevents failures spreading and compounding across independent units of the system. Fault-tolerant API calls between services are a key pattern that prevents a cascade of failure across the distributed system. Along the way, the team carefully balances compartmentalization against redundancy.
- **Scale automatically**. To serve unpredictable load without performance degradation, automatically scale up quickly, and down slowly without relying on slow, fallible human operators, triggered by saturation points of resources such as CPU, memory, or queue depths.
- **Fast rollbacks**. We set rollback targets in minutes for all services, and automatically test rollbacks in pre-production environments by making roll-forward, back, and forward again a default operation. The team makes extensive use of feature flags for even faster, more granular emergency switches and rollouts.
- **Protect all services receiving API calls**. Load-shedding, tenant fair limits, web application firewalls, and sophisticated layer seven protections are deployed at all levels of the system, from our outermost perimeter services exposed directly to the internet, down to the team’s deepest most internal services that can be accidentally attacked by bugs in higher-level calling services.
- **Soften dependencies**. Dependencies between services are designed to be soft wherever possible to allow them to fail or succeed independently. Caching is one of the most common patterns here - often a stale result from a downstream dependency is adequate for continued function.
- **Favor async communication**. Asynchronous, brokered communication between services decouples those services from each other and buffers load spikes between them.
- **Make API calls fault-tolerant**. To be tolerant of partial failures and transient network issues, we use several patterns: timeouts and deadlines, circuit breaking, and retries with backoff. We prefer non-blocking calls when possible to limit resource consumption and blocking. Backwards and forwards compatibility is enforced with schema-level linting at build time and integration testing.
- **Manage service quotas and constraints**. The team sets quotas and constraints across its service fleet, such as IP addresses, disk IOps, or the capacity of a given Kubernetes cluster. The team aggregates, monitors, and alerts against usage of these quotas and constraints centrally to avoid an approaching limit from impacting the system at runtime.

Second, a multi-layered inspection model ensures services meet these standards. This includes automated chaos testing, scanning, and linting for anti-patterns, and architecture reviews with senior architects to catch issues not addressed by automation.

Third, solutions are integrated into Hyperforce to ease adherence to these standards. This includes automatic telemetry collection, default redundancy, and failover mechanisms, and built-in protections like load shedding and DDoS defense, all activated by default for individual services.

Salesforce handles an immense volume of telemetry data, including metrics, logs, events, and traces, which traditional monitoring solutions can’t always manage effectively.

To address this, Salesforce developed a comprehensive observability system that integrates with its software development lifecycle, operations, and support functions. This system provides a unified experience for engineering and customer support teams, while meeting ‌scale needs and reducing licensing costs for third party software.

The metrics infrastructure at Salesforce, built on OpenTSDB and HBase, supports large-scale collection, storage, and real-time querying of time-series data. Non-real-time use cases utilize Trino and Iceberg, handling over 2 billion metrics per minute to provide insights into CPU utilization, memory usage, and request rates. For log management, Salesforce uses Splunk for its powerful indexing and search capabilities. Apache Druid supports real-time ingestion and analysis of large-scale event data, crucial for understanding user interactions and system events. Distributed tracing across microservices is managed with OpenTelemetry and ElasticSearch, aiding in identifying specific latency and failure points.

Salesforce also implemented an Application Performance Monitoring (APM) infrastructure that integrates with its technology stacks for data collection and telemetry stores. This auto-instrumentation of applications simplifies data collection and ensures consistent telemetry across services. APM’s unified dashboard correlates various data types, enhancing the ability for engineers to monitor performance, diagnose issues, and optimize systems through a cohesive interface.

By standardizing observability tools, Salesforce links disparate telemetry types across services using distributed tracing. This creates a comprehensive service dependency graph, visualizing the entire service ecosystem and tracing requests with fine granularity. This capability is crucial for pinpointing issues, identifying bottlenecks, and supporting AI-driven features like anomaly detection, predictive analytics, and automated remediation.

To increase incident resolution times, we’ve developed an AI Operations (AIOps) Agent that automatically detects, triages, and remediates incidents on behalf of human operators, with intervention only in a minority of cases. The AIOps Agent is a scalable multi-agent-reactive toolkit designed to facilitate the development of complex, reactive agent-based systems. It’s highly modular and can be enhanced with various tools to extend its functionality. It’s designed to efficiently scale with increasing numbers of agents. Key features include a reactive architecture, enabling agents to dynamically react to changes in their environment; tool enhancement, allowing for easy integration of tools to extend agent capabilities; and a pluggable planning module, which enables customization of agents’ planning strategies by plugging in different planning modules.

Swift proactive detection is accomplished for 91% (at the time of writing) of our core CRM product incidents with advanced machine learning models from our Merlion library, a publicly available open-source library developed by our AI research team. Merlion is an ensemble of machine learning models like Isolation Forests, Stats, Random Forests, and long short-term memory (LSTM) neural networks that process the extensive telemetry data generated by our systems in near real-time.

79% of incidents (at the time of writing) are automatically resolved by the agent’s actions. Our AIOps Agent can process and triage data vectors such as logs, profiling, diagnostics, time series, and service-specific artifacts to recommend remediation actions. The AIOps Agent controller and planner choose an agent with specific skills to perform actions in production.

For the remaining incidents that require human involvement, the AIOps Agent efficiently triages unresolved issues to the appropriate service teams. It does so by intelligently understanding the nature and context of each incident using the in-house fine-tuned model XGenOps, which is trained on operational datasets like problem records, incidents, JFRs, and logs, ensuring that it is directed to the team with the necessary expertise. This results in over 2800 hours of engineering time saved per week, mitigating the need for engineers to triage unresolved issues.

To manage the risk of outages from nearly 250,000 production changes made weekly, fully automated deployment systems are used to enforce safe change practices, eliminating human error. Off-the-shelf systems weren’t scalable or customizable enough, prompting the development of more tailored solutions.

The custom continuous deployment system ensures safety through multiple layers, following industry-standard blue/green deployment strategies:

- Mandatory testing evidence for each change.
- Initial canary testing of changes.
- Staggered deployment with controlled blast radius.
- Soaking and health checks between deployment stages.
- Mitigating conflict with existing moratoriums and incidents.

Additionally, continuous integration systems have been optimized to run millions of AI-selected tests, enabling rapid releases while minimizing regression risks.

The core architectural principle of the Salesforce Platform is its metadata-driven design. Salesforce engineers create multitenant services and data stores. Each application on the platform is essentially a collection of metadata that tailors how these multitenant services are utilized by individual customers. That’s why a common marketing phrase for the Salesforce Platform is that “everything is accessed with metadata”.

The platform emphasizes structured and strongly-typed metadata. This metadata serves as an abstraction layer between the customer experience and the underlying Salesforce infrastructure and implementations. This approach enhances both the usability and quality of applications. For instance, instead of using SQL schema definitions and queries, customers interact with structured metadata like entities, fields, and records via Salesforce Object (sObject) APIs. This design allows the platform to integrate new data storage technologies or modify existing ones without necessitating application rewrites, thereby supporting continuous development best practices.

![Metadata-Driven Platform](https://architect.salesforce.com/ns-assets/legacy/image3-metadatadrivenplatform.png)

The Salesforce Platform architecture features a “layered extension” approach that supports four key personas in building and extending apps:

- **Salesforce Engineering:** Teams develop native apps like Sales Cloud and Service Cloud, which are deployed across all services and runtimes through an extensive release process. These apps are made available to all tenants through licensing and provisioning mechanisms.
- **External Partners**: Independent Software Vendors (ISVs) and other partners can extend the metadata created by Salesforce to build value-added solutions, such as schema extensions on Sales Cloud data models or additional validation rules for Service Cloud case records. They can package these solutions for distribution to multiple customers.
- **Organization-specific IT Admins and Developers**: They can customize their applications beyond what ISVs offer, tailoring solutions to meet unique business challenges like proprietary or region-specific processes.
- **Individual End Users**: End users can personalize their app experience, such as changing the column order in a list view or setting a default tab.

Each persona can independently iterate on the same application by ensuring that lower layers don’t depend on changes of personas in the higher layers and by upholding strong versioning and backward compatibility contracts.

One feature that highlights the “layered extension” concept is the Record Save Order of Execution, which ensures that business logic from all four layers is applied in a predictable sequence. This allows more specific, higher-layered business logic determined by the org admin or IT developer to appropriately override lower-layered logic during record saving that might be provided by Salesforce or an external partner.

Additionally, the platform’s metadata frameworks utilizes a “Core” runtime and a proprietary Object-Relational Mapper (ORM) with multitenancy built-in, connected to a relational database. This Core runtime enables shared memory state, referential integrity validations, and transactional commits, which prioritizes app stability and enhances the reliability of app deployments. The architecture has been continually evolving to support the growing scale of application complexity. For example, as of October 2025, there are over 85,000 entities defined by Salesforce, and over 300 million custom entities defined by our customers.  
Historically, the Core runtime hosted the majority of platform and app functionality. The current architecture of the Salesforce Platform now includes hundreds of independent, metadata-driven services. The Core runtime remains the single system of record for application metadata, leveraging the unique benefits of a monolithic architecture for metadata management. The relevant metadata is synchronized to local caches in independent services, powering the diverse array of scalable services for application runtimes.

Data is an essential asset for organizations, and Hyperforce provides a reliable foundation for its storage at Salesforce. The key challenge is to store data in a manner that optimizes its utility for applications. The Salesforce Platform has transformed the data layer by accommodating various storage and access requirements. It effectively balances costs, read/write speeds, storage capacity, and data types to meet diverse needs.

As AI and analytics increasingly shape enterprise applications, data has emerged as a pivotal element. Its importance lies in its ability to enable AI and analytics to learn, analyze, make decisions, and automate processes.

Data originates in System of Record (SOR) databases, fulfilling the operational requirements of businesses. It then transitions through various transformations to big data platforms, which are essential for powering AI and analytics-driven applications.

Effective management of data, from transactional information to analytical insights, is crucial for extracting value and supporting sophisticated applications. Salesforce Database (SalesforceDB) stands out as a premier transactional database for managing SOR data, while Data 360 serves as a robust big data platform that enhances AI and analytics capabilities.

Transactional data and metadata is essential to the Salesforce Platform. SalesforceDB is a modern, cloud-native relational database designed specifically for Salesforce’s multitenant workloads, similar to other cloud databases from major providers but with custom features for Salesforce’s architecture. It extends PostgreSQL, separates compute and storage, and leverages Kubernetes and cloud storage, enhancing operations with tenant-specific functionalities like encryption and sandboxes.

SalesforceDB handles all transactional CRM data, upwards of 1.1 trillion transactions per month, as well as metadata for Data 360 and related services. Its primary objectives are to ensure trust through durability, availability, performance, and security; scale for large customers; and facilitate simplified, reliable cloud operations. It achieves these goals with a design that separates compute and storage layers, an immutable, distributed storage system, and log-structured merge tree data access. This enables advanced features like per-tenant encryption of data in storage and efficient sandboxes and migrations.

The SalesforceDB service architecture runs across three availability zones, with compute and storage replicated across these zones to ensure the system remains available even if any node or entire zone is lost. All services run in Kubernetes to enable automated failure recovery and service deployments.

To provide high levels of durability and availability, the ultimate system of record for SalesforceDB is cloud storage like AWS’s S3. Operations such as archiving and cross-region replication are managed at this cloud storage level. Storage objects are immutable, enhancing data distribution and replication for high availability.

Due to high latency in cloud storage, SalesforceDB uses storage caches to access data. These caches are distributed storage systems that maintain temporary copies of storage objects in a cluster of nodes, ensuring replication and durability as needed by the database. Separate caches are used for transaction log storage and data file storage.

The SQL compute tier consists of a primary database cluster and two standby clusters in three different availability zones. The primary cluster handles all database modifications, while the standby clusters only handle query operations.

![Transactional Database](https://architect.salesforce.com/ns-assets/legacy/image5-transactionaldatabase.png)

SalesforceDB utilizes a log-structured merge tree (LSM) data structure, where changes are initially recorded in a transaction log and accumulated in memory. The committed changes are then collectively written out into key-ordered data files, which are periodically merged and compacted to optimize storage efficiency.

This structure effectively eliminates concurrent-update issues that are common in databases that update storage directly. By using the LSM approach, SalesforceDB supports critical features such as immutable storage, making it a robust solution for managing Salesforce workloads.

Data in storage is immutable; once data files are written and made visible, they don’t change. Transaction logs are append-only, simplifying data access patterns and enhancing reliability. This structure supports uncoordinated reads, simplifies backups, boosts scalability, and facilitates storage virtualization, making it well-suited for cloud environments.

Transactions in SalesforceDB are committed across multiple availability zones, which ensures that there is no data loss even if a node or zone fails. If a failure occurs, in-flight, transactions are aborted, and committed transactions are successfully recovered. Since failures don’t lose committed data, failover to new nodes is automated.

Cluster management software automatically handles failovers by monitoring quorums and managing ownership transfers. This process isn’t only used in emergencies but also routinely during regular patching, enhancing the system’s reliability through constant use. Short database restarts are typically unnoticed by end users, maintaining a seamless user experience.

Salesforce does three major schema updates per year, with smaller schema updates weekly. SalesforceDB provides zero-downtime schema operations that enable these updates to be done with no customer impact.

Our transactional database serves as the primary repository for customer data, which is cached across multiple availability zones and stored in the cloud. Each data block is secured with an immutable checksum, verified by both the storage layer and the database engine. The database performs lineage tracking to detect any out-of-order changes or missed versions and runs ongoing consistency checks between indexes and base tables.

For ransomware protection, databases are archived in separate storage under a different account, including both full and incremental transaction log backups. These backups are regularly validated through a restoration testing process. Additionally, cloud infrastructure is pre-configured but not activated, ready to manage data restoration requests as needed.

Each Salesforce org is housed in a Hyperforce cell, which includes the SalesforceDB service. This setup allows for rapid global scaling through the creation of new cells via the Hyperforce architecture, and traffic can be easily shifted between cells to manage load. However, as customer workloads and business demands increase, the capacity of a single database instance may be insufficient.

To address this, SalesforceDB employs a horizontal scaling architecture for both its storage and compute tiers. Cloud storage is virtually unlimited, and the cache layers automatically scale to meet demand. Additionally, the compute tier can expand by adding more database compute nodes, which efficiently read from shared immutable storage without needing coordination. This approach allows SalesforceDB to achieve scalability that matches or exceeds that of leading commercial cluster database architectures, without requiring special networking or hardware.

Salesforce is a multitenant application where a single database hosts multiple tenants. Each table record includes a tenant ID to distinguish its ownership, and tenant isolation is maintained through automatic query predicates added by Salesforce’s application layer.

SalesforceDB is tailored to this model, supporting tenant-specific DDL, metadata, and runtime processes, enhancing reliability, performance, and security. It combines the low overhead of a tenant-per-row model with the efficiency of a tenant-per-database schema.

In SalesforceDB, tenant IDs are part of the primary key in multitenant tables, which cluster data by tenant in the LSM data structure, enhancing access efficiency. This setup not only facilitates efficient data access and per-tenant encryption but also simplifies tenant data management. Tenants can be easily copied or moved with minimal metadata adjustments due to the compact metadata structure.

AI, analytics, and data capabilities are essential in modern enterprises. Enterprises already invest in mature big data platforms such as Snowflake, Databricks, BigQuery, and Redshift. However, many  
customers are not deriving business value out of their data due to data silos, lack of AI processing, stale data or inaction within an existing business process. Centralizing customer data into a single source of truth, with a single view of customer engagement, is both crucial to a business and challenging due to data fragmentation and the complexity of system management. Salesforce leads in facilitating a holistic view of a customer by integrating data, AI, and CRM into a virtuous circle, driven by generative AI and machine learning insights and powered by data.

SalesforceDB is optimized for high-performance transactional workloads on structured data, whereas AI and analytics workloads require handling large volumes of unstructured data from various sources and performing complex queries and batch processing. To address these needs, Salesforce has developed Data 360, a platform designed to break down data silos, unify, store, and process data securely and efficiently, supporting AI and analytics demands, and enabling real-time enterprise operations.

![Data 360 and Data Lake](https://a.sfdcstatic.com/developer-website/prod/images/architect/Data360-data-lake.png)

Data 360, built on Hyperforce, serves as the foundational platform for AI and Analytics, offering:

- Integrated infrastructure and a no-code platform to consolidate data silos through connections
- Real and near real-time data ingestion
- Zero-copy federation
- Data cleansing, preparation, and shaping for processing
- Unified Query Service over structured and unstructured data
- Development of analytical and AI/ML models for insight generation
- Data-triggered actions and activations
- Support for generative AI retrieval augmented generation (RAG)
- Comprehensive Policy based Governance

Data 360 Architecture supports a number of components and capabilities, which are outlined below.

Data 360 supports efficient ingestion pipelines from various structured and unstructured data sources, for batch, near real-time, and real-time data processing. Data 360’s ingestion service operates on an Extract-Load-Transform (ELT) pattern, designed for low-latency and suitable for B2C scale. Real-time ingestion includes APIs and interactive streams, while near real-time sources cover detailed product usage. Once ingested, data is extensively transformed to prepare, harmonize (for example, unifying various contact types), and model it for effective querying, analytics, and AI applications. The platform also includes a wide range of ready-to-use harmonized data models.

Data 360 integrates seamlessly with Salesforce applications such as Sales Cloud, Service Cloud, Marketing Cloud, and Commerce Cloud. Additionally, it offers hundreds of connectors for external data sources, ensuring smooth data integration.

Data 360 features a native lakehouse architecture based on Iceberg/Parquet, designed to handle large-scale data management and processing for batch, streaming, and real-time scenarios. This architecture supports both structured and unstructured data, crucial for AI and analytics applications.

![Lakehouse for Big Data](https://architect.salesforce.com/ns-assets/legacy/image7-lakehouseforbigdata.png)

In cloud-based data lakes like Azure, AWS, or GCP, the fundamental storage unit is a file, typically organized into folders and hierarchies. This lakehouse enhances this structure by introducing higher-level structural and semantic abstractions to facilitate operations like querying and AI/ML processing. The primary abstraction is a table with metadata that defines its structure and semantics, incorporating elements from open-source projects like Iceberg or Delta Lake, with additional semantic layers added by Data 360.

Abstraction Layers in the lakehouse:

- **Parquet File Abstraction**: At the base, storage consists of data lake files (for example S3 in AWS or Blob in Azure) in Parquet format. Data for a source table is stored across multiple partitions as Parquet files, with each table being a collection of these files.
- **Iceberg Table Abstraction**: Tables are organized as folders, with data partitions stored as Parquet files within these folders. Modifications to a partition result in new Parquet files as snapshots. Iceberg manages a metadata file for each table, detailing schemas, partition specs, and snapshots.
- **Salesforce Cloud Table Abstraction**: Building on Iceberg, this layer adds semantic metadata such as column names and relationships, along with configurations like target file size and compression. It abstracts tables across various platforms like Snowflake and Databricks, shielding Data 360 applications from underlying storage platform specifics.
- **Lake Access Library**: This library provides access to the Salesforce Cloud Table, handling both data and metadata, and abstracts the underlying storage mechanisms for application developers.
- **Big Data Service Abstraction**: This includes processing frameworks like Trino and Hyper for querying, and Spark for processing across any cloud table platform.

Data 360 Lakehouse supports B2C scale, real-time ingestion, processing, schema enforcement and evolution, snapshots, and uses open storage formats.

To support real-time analytics and agentic applications, Data 360 augments a lakehouse’s big data storage with an additional Low Latency Store (LLS). Data 360’s real-time processing layer analyzes real-time signals and engagement data in memory. As memory-based storage capacity is limited, all data cannot be processed at once. Data 360 adds this LLS to remove such limitations, enabling scalable real-time processing.

The Low Latency Store is a petabyte scale NVMe (SSD) storage layer on the lakehouse. It is a durable cache – most data eventually makes it to the lakehouse for long term persistence. In-session data in the real-time layer can be flushed to the low latency store for subsequent fast access. For example, in an agentic conversation, recent messages can be processed in memory; older messages can be flushed to the LLS. If a previous conversation is required, it can be accessed within a few milliseconds from the LLS. NVMe-based storage allows for large amounts of data to be stored and accessed at millisecond latencies. Data may make its way to the lakehouse for long-term persistence.

In addition, data from the lakehouse that is required for real time processing or to augment real time experiences is retrieved and kept in the LLS. For example, customer profile context is pre-fetched or brought from the lakehouse and cached in the LLS. Also, any lakehouse objects and other objects that are required for real-time processing during in-session processing can also be cached in the LLS. The LLS enables a real-time layer on a true storage hierarchy with memory, SSD and lakehouse storage layers, with data seamlessly migrating between each.

Data 360 also offers robust support for security, including Tenant-Level Encryption (TLE) with customer-managed keys, as well as privacy and compliance through its governance technologies. At the core is attribute-based access control (ABAC) support, which dynamically evaluates access based on attributes related to entities, operations, and environmental factors. This system supports both discretionary and mandatory access controls.

Complementing ABAC, a detailed data classification system categorizes data by sensitivity and purpose, enhancing compliance, risk management, and incident response. Together, ABAC and this classification system provide comprehensive data governance, ensuring data within Data 360 is managed securely and efficiently.

Data 360 integrates deeply with the Salesforce Platform for metadata, packaging, extensibility, user experience, and application distribution via AppExchange. Customers can define and manage the metadata for lakehouse streams and tables, just like other Salesforce metadata. Every data object (including federated or external tables) is represented as a Salesforce object, and modeled as virtual entities backed by data storage in Data 360. They can be used by developers to build applications on the Salesforce Platform.

Data 360 offers extensive support for zero-copy federation, allowing users to integrate with external data warehouses like Snowflake and Redshift, lakehouses such as Google BigQuery, Databricks, and Azure Fabric, as well as SQL databases and various file types including Excel. Data 360 supports file and query-based federation, with live query and access acceleration as shown in the figure. Labels (1) and (2) illustrate Data 360’s query (including live query pushdowns) and file-based federation for accessing data from external data lakes/warehouses/data sources; and label (3) highlights acceleration of federated access from external data lakes/data sources. Labels (4) and (5) illustrate query and file-based sharing of data from Data 360 with external data lakes/warehouses. capability also extends to unstructured data sources like Slack and Google Drive, which can be accessed by Data 360’s unstructured processing pipelines. Additionally, Data 360 facilitates the abstraction of Salesforce objects and data access for data federated from external sources, enabling access to such data across the Salesforce platform and applications.

![Zero Copy Federation and Extensibility](https://a.sfdcstatic.com/developer-website/prod/images/architect/zero-copy-data-federation-data-flow-diagram.png)

Data 360 integrates a CDP that features advanced identity resolution capabilities, creating unified individual identifiers and profiles along with comprehensive engagement histories. This platform is adept at handling both business-to-business (B2B) and business-to-consumer (B2C) frameworks by supporting identity graphs that utilize both exact and fuzzy matching rules. These identity graphs are enriched with engagement data from various channels, which helps in building detailed profile graphs with valuable analytical insights and segments.

Additionally, the CDP enables effective segmentation and activation across different platforms such as Salesforce’s Marketing Cloud, Facebook, and Google. It processes customer profiles in batch, near real-time, and real-time, which allows for immediate decision-making and personalization. This functionality enhances interactions in both B2C and B2B scenarios, ensuring that businesses can respond swiftly and accurately to customer needs and behaviors.

Data 360 offers an enterprise data graph in JSON format, which is a denormalized object derived from various lakehouse tables and their interrelationships. This includes a "Profile" data graph created by CDP that encompasses a person’s purchase and browsing history, case history, product usage, and other calculated insights, and is extensible by customers and partners. These data graphs are tailored to specific applications and enhance generative AI prompt accuracy by providing relevant customer or user context.

Additionally, plans are in place to expand these data graphs to include knowledge graphs that capture and model derived knowledge, such as extracted entities and relationships from unstructured data. The real-time layer of Data 360 utilizes the Profile graph for real-time personalization and segmentation.

![Real-Time Layer](https://architect.salesforce.com/ns-assets/legacy/image9-real-timelayer.png)

Data 360’s real-time layer is engineered to process events such as web and mobile clickstreams, visits, cart data, and checkouts at millisecond latencies, enhancing customer experience personalization. It continuously monitors customer engagement and updates the customer profile from CDP with real-time engagement data, segments, and calculations for immediate personalization.

For example, when a consumer purchases an item on a shopping website, the real-time layer quickly detects and ingests this event, identifies the consumer, and enriches their profile with updated lifetime spend information. This allows for the personalization of their experience on the site in sub-seconds. Additionally, this layer includes capabilities for real-time triggering and responses, enabling immediate actions based on customer interactions.

Personalization is knowing which persona to target, when and where to deliver relevant content and recommendations, what to say and at what frequency. The Personalization Services Platform capability of Data 360 is the orchestrator of ‌which decisions are made to optimize goal achievement through personalized experiences. This platform provides the following capabilities:

- Consistent set of models and ways to interpret profile, activity, and asset data in Data 360.
- Platform-integrated experimentation (for example, A/B/n or multi-arm bandit decision making).
- Integration of goals at design time via configuration, ML training time and runtime (ML inference).
- B2C scale, real-time and batch interaction support (anonymous users, high-volume real-time/interactive external, high-volume internal batch).
- Analytics driven through Data 360.
- Patterns to integrate AI models and service from other parties (both internal and external).
- OOTB implementations of high-value AI-driven use cases (recommendations and decisions with various ML algorithms, including contextual bandits for promotion/content selection, product recommendations and pricing decisions).

Data 360 is an active platform that supports the activation of pipelines in response to data events. For instance, a significant event, such as a drop in a customer’s account balance can trigger a Salesforce Flow to orchestrate a corresponding action. Similarly, updates to key metrics, such as lifetime spend, can be automatically propagated to relevant applications.

Data 360 features elastic scaling compute clusters that efficiently handle processing tasks. It offers robust management for both multitenant and dedicated compute environments. Additionally, it provides managed support for Spark and SQL. BYOC (Bring Your Own Compute/Code) features support multiple programming languages, including Java, Python, and Spark, allowing for the integration of custom transforms, models (including LLMs), and functions, enhancing extensibility.

Data 360 Compute Fabric provides a unified layer known as Data Processing Controller (DPC) for managing and executing all big data workloads. DPC is a comprehensive, multi-workload data processing orchestration service that provides Job-as-a-Service (JaaS) capabilities across diverse cloud compute environments. It abstracts infrastructure complexity and unifies job execution for frameworks like Spark (EMR on EC2 and EMR on EKS) and Kubernetes Resource Controller (KRC) workloads. By serving as a centralized control plane gateway, DPC orchestrates, schedules and monitors jobs across multiple data planes, ensuring reliability, scalability, cost efficiency and a consistent developer experience.

Data 360’s Query Service provides advanced querying capabilities, featuring extensive SQL support for both structured and unstructured data via Trino and Hyper. It enhances functionality with operator extensibility through Table Functions, allowing for diverse search operations across text, image, spatial, and other unstructured data types. These capabilities are seamlessly integrated with relational operations, such as selecting customer records. This unified approach enables the generation of targeted and personalized results, facilitating more precise LLM responses using RAG.

Data 360 supports storage and management of structured (tables), semi-structured (JSON), and unstructured data seamlessly across data ingestion, processing, indexing, and query mechanisms. Data 360 supports various unstructured data types beyond text, including audio, video, and images, broadening the scope of data handling and analysis. The figure below illustrates the two sides of grounding (ingestion and retrieval).

![Unstructured Data Processing](https://a.sfdcstatic.com/developer-website/prod/images/architect/unstructured-data-storage-and-processing.png)

Data 360 manages unstructured data by storing it in columns as text or in files for larger datasets. It supports data federation for unstructured content, which allows for the integration and management of data from multiple sources.

Data 360’s unstructured data indexing pipeline is designed as a modular, extensible architecture comprising five core stages: Parsing, Pre-Processing, Chunking, Post-Processing and Embedding. These stages are then followed by keyword and vector indexing. Examples of Pre-Processing include operations such as noise elimination, language normalization, and image understanding (Optical Character Recognition), while Post-Processing stages may include metadata enrichment, semantic grouping, or advanced techniques such as chunking.

Data 360 provides multiple out-of-the-box and pluggable models for chunking and embedding generation. Data pipelines in Data 360 fully support code extensions, allowing customers and internal teams to plug in custom logic at any stage. These stages also support LLM-based processing, which allows customers to define their own prompts as needed.

For indexing, Data 360 supports keyword indexing utilizing search services, and vector indexing utilizing Milvus; an open-source native vector index. For setting up RAG with unstructured processing, Data 360 leverages context indexing to enable rapid iteration and quick validation utilizing sample test queries, with persona-specific content configured to tailor to the consuming persona or user.

The Document AI capability of Data 360 supports reading and importing unstructured or semi-structured data from documents like invoices, resumes, lab reports, and purchase orders. This feature supports ad-hoc interactive processing, as well as bulk batch processing. This is a key capability that enables business process automation for our customers.

Data 360 features a headless Semantic Layer with APIs designed to enhance business semantics and AI/ML-driven analytics, similar to Tableau Next. This layer includes a semantic data modeling service that enriches traditional analytical models with business taxonomy such as measures and metrics.

Its semantic query service utilizes a declarative language to interact with these models, translating queries into SQL for accessing data from both native and federated data sources within Data 360.

This integration facilitates scalable and interactive analytical explorations, reports, and dashboards, compatible with third-party visualization tools.

Data 360 functions as a centralized governance hub, ensuring that all data, from raw ingestion to activated insights, is managed with integrity and control. Data 360 has adopted Attribute-Based Access Control as its core authorization model. ABAC allows access decisions to be based on attributes of the user (department, role, location), data (personal information, sensitivity, data space), and environment (for example, time of day), rather than predefined roles. This enables highly granular and contextual access policies that adapt as data and user attributes change. At the heart of Data 360's ABAC implementation is the use of the CEDAR policy language. This purpose-built, open-source, formal policy language provides a precise and verifiable way to define complex authorization rules, ensuring that policies are unambiguous and can be evaluated consistently at scale.

The governance lifecycle includes key capabilities regarding policy information, enforcement and decision points:

- **Tagging and Classification (Policy Information Point):** Data is identified and enriched with critical attributes. Data 360 provides automated tagging and classification mechanisms, leveraging discovery, LLMs, and machine learning to identify sensitive data categories (for example, personally identifiable information such as email, phone, name) in both structured and unstructured data.
- **Authorization Service (Policy Enforcement Point):** This service intercepts all data access requests from various consumption layers (hybrid structured/unstructured queries, RAG retrievers & prompts, and CRM enrichment) and consults the Policy Decision Point to determine if access is permitted.
- **Policy Evaluation Engine (Policy Decision Point):** This engine takes the access request context from the Policy Enforcement Point, along with policy definitions (in CEDAR), and attributes from the Policy Information Point, to make an authoritative access decision.

The ABAC framework with CEDAR policies provides control and flexibility, ensuring that customer data is not only actionable but also secure, compliant, and trustworthy across the enterprise.

Caches are essential for fast access to frequently used data. Salesforce uses many caches across the Salesforce Platform, including in Core Application Servers, SalesforceDB, and at the Edge. The Salesforce Platform and applications need a scalable, tenant-aware caching solution with low latency and high throughput. This solution must allow Salesforce engineers to control what’s cached and for how long, ensuring that their data is not evicted by system noise or other customers’ data. Vegacache, a Salesforce-managed caching service based on Redis, is tailored for a polyglot, multitenant, and public cloud environment. It’s widely used by Salesforce services and accessible to platform developers via Apex programming language APIs. Operating at scale in Hyperforce, as of writing, Vegacache handles over 2 trillion requests daily with sub-millisecond response times.

Vegacache instances, running in Kubernetes containers accessed via Service Mesh, are deployed across multiple Availability Zones to balance data availability and latency. It scales automatically based on system load, ensuring data availability and slot ordering preservation. Vegacache provides guaranteed cache size per customer and offers protection against noisy neighbors, with resilience against infrastructure failures through replicated data storage.

For the Salesforce Platform developers, Vegacache makes it possible for developers to cache Apex Objects and SOQL database query results, reducing CPU usage and latency by eliminating unnecessary data fetches from SalesforceDB. It supports Put(), Get(), and Delete() operations, keeping frequently used objects readily accessible.

Salesforce natively supports asynchronous data processes and architectures for enhanced workflow flexibility, resiliency, and scalability.

Salesforce engineers first leveraged message queues to decouple bulk and large data processes, as well as coordinate processes between independent systems. These message queues were abstracted from the external developer via platform features, like Bulk API queries or Asynchronous Apex. The Salesforce Platform then introduced log-organized event streams built on a robust messaging infrastructure of internally managed Apache Kafka clusters. This enabled an event-based architecture with a publish/subscribe interaction model, and was productized to external developers as Platform Events.

Both message queues and event streams continue to be highly-leveraged technologies of apps and solutions built on the platform, especially as they leverage more features, clouds, and external systems hosted on independent runtimes. Communicating via versioned event schemas enables independent software development lifecycles for the different runtimes. The decoupling of systems via events also helps manage load spikes and elasticity/scale of individual runtimes to support a higher overall resiliency and availability of an app.

Search features at Salesforce, crucial for applications ranging from global search to generative AI, face unique challenges that shape our architectural approach:

- **Scale**: Supporting hundreds of thousands of customers and millions of tenants, our cloud-native search solution is designed for massive scale while remaining cost-effective.
- **Customer Diversity**: Salesforce’s diverse customer base across various industries has unique and complex search requirements due to extensive customization of the platform, involving numerous object types and fields.
- **Operability**: The search solution must be resilient and highly available, supporting data residency, tenant lifecycle operations like regional migrations, and sandboxing, and maintain low-indexing latency with fairness between tenants.
- **Relevance at Scale**: Enhancing the relevance of search results to meet diverse user queries is critical, especially as we scale relevance algorithms to accommodate various tenants, data types, and search scenarios.
- **AI and Semantic Capabilities**: Search supports Machine Learning and generative AI, particularly for Retrieval-Augmented Generation (RAG) and Agentic Search.
- **Seamless Integration**: To ensure a cohesive user experience, Salesforce’s search technology integrates deeply with the broader Salesforce Platform, including metadata models and AI/data services.

Salesforce’s cloud-native solution, SeaS (Search as a Service), is built on Solr, an open-source distributed search engine. Salesforce has significantly extended and optimized Solr to meet our unique challenges and has integrated it deeply with Salesforce applications and platform, incorporating semantic technologies to enhance AI applications and search relevance.

SeaS employs a compute/storage separation architecture, allowing for scalable distribution of indexes across nodes and rebalancing loads and availability across zones during failures. It features automatic sharding and resizing of shards, zero-downtime upgrades, and optimizations like replica lazy loading and archiving to cater to rarely used indexes.

The architecture also includes a low-level index implementation optimized for a large number of fields, auto-complete, spell-correction, and bring-your-own-key encryption. Managing around 6,000 Solr nodes globally, Hyperforce search infrastructure uses multiple independent clusters (Hyperforce cells) in each region to balance cost and control, automatically placing client indexes based on load, domain, and type.

Salesforce’s search relevance pipeline employs learning-to-rank techniques, adapting to the diverse needs of our customers and supporting features such as result ranking. It also includes entity predictions from user queries and past interactions. Relevance models are continuously refined by learning from user interactions and evaluated through A/B testing, enhancing search result accuracy. This process also supports bootstrapping models for AI applications via knowledge transfer.

The stack incorporates a vector search engine for semantic search and AI applications, integrated with Data 360 for generative AI capabilities. This includes a comprehensive pipeline for data transformation, hybrid search support, a catalog of configurable rankers, such as the Deep Fusion Ranker and Autodrop to filter out low-relevance search results.

As generative AI is shifting the primary consumer of search services from human users to use LLMs, the Salesforce search stack is adapting to find and return results optimized for this programmatic consumption, dealing with longer and more complex queries and returning more descriptive results like chunks. This supports new Agentic Search capabilities, where Agentforce agents leverage search with a reasoning loop to accomplish complex tasks.

Salesforce’s search features span various contexts, including global search, lookups, search answers, community search, related lists, setup, mobile and generative AI applications. This broad functionality is achieved through tight integration of the Search stack with Salesforce’s metadata system and UI ecosystem, enabling seamless support for both standard and custom objects.

Additionally, integration with Data 360 enhances search capabilities on data objects through no-code configurations and allows for the composition of search functions within data pipelines, such as including search statements in SQL queries. The Search stack leverages Data 360 rich connectors ecosystem, like the Google Drive permission-aware connector, to provide a complete enterprise search capabilities. The integration extends to the AI Platform, enabling search queries to be used as retrievers in Prompt Builder for grounding and in Agentic Search.

AI has reshaped the technology landscape, and the Salesforce Platform, with its integrated and rich data layer, positions Salesforce to deliver impactful AI experiences to customers. Salesforce began its AI transformation nearly a decade ago and has led the field since 2013, focusing on research, ethics, and product development to empower businesses to solve complex problems and drive growth.

Leveraging the core value of Innovation, Salesforce introduced Einstein Predictive AI, enabling businesses to analyze data, automate processes, understand customers, and optimize operations with a comprehensive suite of AI-powered tools such as Einstein Prediction Builder and AI bots. With the rise of Generative AI, Salesforce launched Agentforce, a platform that merges predictive and generative models to offer advanced AI capabilities while prioritizing data privacy.

With the most recent launch of Agentforce 3.0, built on Python with an event-driven framework, Salesforce introduces enhanced flexibility through features like built-in conversation history, end-to-end session tracing, voice support, and custom reasoning engine (Bring Your Own Planner) functionality, enabling more scalable, customizable, and intelligent multi-agent systems.

Agentforce follows these core principles:

- **Data Security and Ethics**: Prioritizes data protection, compliance, and ethical AI principles.
- **Transparency and Explainability**: Offers clear understanding and validation of AI-generated outputs.
- **Flexibility and Customization**: Tailors AI applications to specific needs and industries.
- **Seamless Integration**: Integrates with Salesforce CRM and other systems.
- **Scalability**: Handles large-scale deployments and delivers real-time AI experiences.
- **Intelligent and Consistent Experiences**: Provides personalized, augmented, and automated experiences through connected data and contextual understanding.
- **Comprehensive Observability:** Provides deep visibility and monitoring into AI agent interactions to enable proactive optimization and fine-tuning of agents using Agentforce Interaction Explorer.
![AI Architecture Overview](https://a.sfdcstatic.com/developer-website/prod/images/architect/architecture-overview-ai.png)

The AI stack consists of several key components:

- **AI Platform**: This platform layer is responsible for managing, training, and fine-tuning AI models used in both predictive and generative applications. It offers out-of-the-box (OOTB) services, trust services and foundational models for training, testing, and performing inference on models. Additionally, it supports the integration of your own predictive and generative models, allowing you to bring custom models within the platform.
- **AI Foundational Services**: This includes the AI Gateway, Feedback Framework, RAG, Agentic Orchestration, Agent Evaluation and Reasoning services, which facilitate the integration of business applications with the AI stack.
- **AI-Powered User and Agent Experiences**: Salesforce delivers specialized AI-powered applications through its cloud services. Customers can also create custom experiences leveraging any component of the platform—such as Flow, Apex, or even Lightning Web Components (LWC)—to create AI-powered experiences seamlessly integrated into their workflows and business processes.
- **Agentforce Studio**: This component features tools like Agent Builder, Prompt Builder, Testing Center and Model Builder, designed for creating both generative and predictive AI experiences. It offers end-to-end support for developing/training, testing, and tuning AI models. Next Gen Authoring enhances these capabilities, designed to simplify and accelerate AI agent building with improved UX and compatibility with SFDX.
![Agentforce Trust Layer](https://a.sfdcstatic.com/developer-website/prod/images/architect/foundational-concepts-agentforce-trust-layer.png)

The Agentforce Trust Layer is available in select use cases to help safeguard customer data in generative AI applications by offering robust features:

- **Data Privacy**: Strong masking and privacy controls protect sensitive information from being accessed by external AI models.
- **Security**: Ensures a secure data processing environment and prevents unauthorized access.
- **Trust**: Maintains customer control over data, with no third-party AI storage or usage.
- **Guardrails:** Enforce agent behavioral standards and mitigate the inherent nondeterminism of LLMs, verifying agents consistently follow predefined instructions and workflows.
- **Accuracy**: Enhances AI outputs by using relevant Salesforce data to ground prompts.
- **Content Moderation**: Offers both pre- and post-content moderation, customizable data masking for sensitive information (PII/PCI/PHI), and toxicity classification for large language model (LLM) responses.

The AI Gateway provides a unified interface for accessing and managing various LLMs and predictive models. It acts as a bridge between Salesforce and the world of LLMs, abstracting the complexities of different LLM providers and customers’ own predictive AI models, offering a consistent way to interact with them. The Agentforce AI Gateway integrates with multiple LLM providers, allowing customers to choose the best model for their needs, and incorporates robust data security measures to help manage costs associated with using different LLMs.

Feedback Service is a component that collects, analyzes, measures, and utilizes user feedback to retrain and refine AI models. It plays a crucial role in the continuous improvement of AI-driven features and functionalities within the Salesforce Platform.

RAG is a vital technique that enhances search capabilities with generative AI, leading to more informative and accurate responses. Utilizing the extensive Salesforce Data 360 and the integrated Vector Database, the Agentforce platform quickly retrieves relevant data for a user’s query. This data is then used as grounding for LLMs to generate optimal responses.

Additionally, this method boosts response speed and user trust by including source data in responses. RAG is extensively employed in the Agentforce platform, particularly for applications like Agentforce for Service and Agentforce for Sales, highlighting how it surfaces relevant information for these use cases.

As AI models advance, the development of agents to automate tasks that require reasoning is the next step. These agents serve as intelligent assistants, capable of understanding and responding to queries in natural language, allowing users to design, test, and deploy them for various tasks. A crucial component of this system is the Planner Service, which functions as follows:

- **Interprets User Request**: It analyzes the user’s input to determine intent.
- **Builds a Plan**: It formulates a structured plan to address the user’s needs.
- **Launches Actions**: It executes the plan by initiating actions directly or through other services.

The Planner Service orchestrates the process, ensuring that the agent efficiently fulfills user requests by managing and executing the necessary steps.

Agentforce represents a platform for building agents, enabling customers and ISVs to create automated AI agents for applications like Service Agents and Sales Agents. These agents can process and respond to customer inquiries in a natural, human-like manner, handling a broad spectrum of business tasks, and delivering significant benefits to both businesses and their customers.

The workflow of an agent includes:

- **Activation**: The agent is triggered by predefined criteria such as a customer’s request across various channels.
- **Understanding and Responding**: It employs Natural Language Processing (NLP) to grasp the customer’s query, intent, and sentiment, then consults Salesforce’s knowledge base or other data sources to craft an appropriate response.
- **Handling Complexities**: If faced with a complex issue or needing human oversight, the agent can smoothly hand over the interaction to a human agent.
- **Continuous Learning**: The agent learns from each interaction, continuously enhancing its responses and overall performance.

Agentforce Studio provides a low-code platform that enables customers to integrate AI into their Salesforce applications and workflows, making AI technology accessible beyond data scientists.

Key features of the studio include:

- **Model Builder**: Allows building or importing AI models tailored to specific business needs.
- **Prompt Builder**: A no-code/low-code tool that facilitates the creation and management of generative AI prompts, enhancing user experience with a simple interface for building, testing, and deploying prompts.
- **Agent Builder**: Enables customers and ISVs to develop customized conversational and autonomous agents.
- **Testing Center**: Supports testing of models, prompts, and agents, crucial for ensuring high-quality AI applications and optimizing performance and cost-effectiveness, while enhancing deterministic responses and the quality of user experience.

Agentforce combines predictive and generative AI, leveraging the unified metadata framework of the Salesforce Platform and Data 360 to deliver intelligent, personalized, and effective business solutions.

To meet the accelerating demands of the generative AI market—including rapid advances in reasoning, the need for scalable multi-agent systems, and the shift toward multimodal interfaces—Salesforce is evolving its architecture with Agentforce 3.0. This next-generation platform is built on several key advancements:

- **Asynchronous, Event-Driven Architecture:** Agentforce 3.0 is built on a Python foundation with an enhanced event-driven framework. This enables asynchronous and highly scalable agent implementation, improving performance and laying the foundation for complex, multi-agent use cases where agents can communicate via events.
- **Multimodal Voice Capabilities:** Moving beyond text-based interactions, Agentforce 3.0 introduces support for voice as a primary modality. The architecture integrates with telephony providers and WebRTC gateways to handle real-time audio streaming. New services manage the conversion of audio to text (ASR) and text back to audio (TTS), enabling natural, conversational voice experiences for use cases like automated contact centers.
- **Agentforce Script and Determinism:** A state-machine-based interception mechanism that constrains agent behavior within an explicitly defined structure, ensuring consistent execution paths. This enables deterministic graphs, provides robust state management to prevent memory loss, and facilitates conditional and LLM-determined handoffs, thereby ensuring predictable and consistent agent actions for critical business processes.

The Salesforce Platform’s App Ecosystem is distinguished by its integration of capabilities across App Platform Services, API, User Experience, and Developer Experience layers. App Platform Services are common capabilities that are used to build and customize most apps on the Salesforce Platform, whereas business capabilities are generally more solution-specific.

The app ecosystem is built on five key capabilities, which guide the app development process.

- **Tenancy**: This involves the logical separation of data and metadata within a multitenant service, allowing authenticated users to access specific data and functionalities. This is most visible to customers when they receive a Salesforce Org upon registration.
- **Entities**: Representing database tables, entities consist of fields similar to table columns. Entity and Field metadata includes attributes for data modeling like data types and API names, as well as functional attributes, like if the entity is query-able or write-able. This abstraction, rather than direct manipulation of the data store itself, allows Salesforce to seamlessly introduce and switch storage technologies without requiring updates from IT developers, ensuring continuous app functionality.
- **Access Controls**: These controls regulate user access to data and features, primarily based on user identity and specific policies. Policies are made up of rules and feature toggles, and govern the entities, fields, and features that can be accessed. The policies and permissions are captured in “permission sets”, and access is granted by assigning permission sets to user identities.
- **Layered Extension**: As previously discussed, this supports the independent development of metadata and apps by different roles including Salesforce engineers, external partners, IT admins, and end-users, facilitated by structured save orders and metadata namespaces.
- **Packaging**: This feature allows for the bundling and distribution of metadata across Salesforce tenants, streamlining the update and distribution process of apps without the need for rebuilding.

Beyond these key capabilities, App Platform Services also includes:

- **Data Runtime and Query**: Supports operations like creating, updating, deleting, and querying data across several specialized data stores. A spectrum of data scale and performance is supported by an architecture that enables running data operations directly on the data store, via an internal abstraction for Salesforce engineers to use, or via the customer-facing “Salesforce Object”, or sObject convention.
- **Flow / Workflow / Formulas**: Definition and execution of business logic and validation rules using low-code tools.
- **Apex Code**: Pro-code language for app logic, natively integrated with platform data runtimes and APIs.
- **Cloud-Native Infrastructure Services:** Heroku provides a robust environment for developers using industry programming languages and frameworks to build, deploy, and manage applications that integrate with Platform data and events.
- **Events and Notifications**: Manages triggers and event-based orchestration.
- **Globalization**: Provides support for multilingual and multinational apps.
- **Licensing and Provisioning**: Handles the purchasing and management of access to platform capabilities and apps.
- **Lightning Web Stack**: Allows customization of visual interfaces using structured metadata, like layouts, and standard web technologies.
- **Sites + CDN**: Ensures low-latency and high-traffic web experiences, including for unauthenticated users.
- **Security and Compliance**: Offers tools and controls for meeting specific organizational security and compliance requirements.
- **Data Loss Prevention**: Includes features for data backup, restoration, and archiving.

The Salesforce Platform provides a suite of tools and capabilities via Heroku that enable developers to build, run, and manage applications in the cloud using the programming languages and frameworks of their choice. Heroku’s managed Cloud Application Platform provides application runtimes, data stores, messaging queues, and eventing systems as scalable services to build extensions to Salesforce applications.

Applications running on Heroku have access to the full suite of Salesforce capabilities, customer data, and business logic, and the ability to connect with third-party systems and services. With Heroku, developers can focus on delivering value without being burdened by underlying infrastructure concerns.

Automation is what makes an app dynamic and is crucial for the digital transformation of essential business processes.

Salesforce Process Automation was created to address key challenges faced by customers, including the need for streamlined and efficient business processes as organizations scale. These challenges often involve workflows that require excessive manual effort, leading to inefficiencies and higher operational costs. Customers seek a solution that can automate these processes, minimize manual labor, and maintain consistency and accuracy.

A significant issue was the absence of a user-friendly tool that allowed non-technical users to design and implement business processes without extensive coding skills. Moreover, there was a need for a solution that could integrate securely, scalably, and seamlessly with existing automated Salesforce tasks such as data entry, approvals, notifications, and complex multi-step processes.

Salesforce Process Automation meets these needs by offering a robust yet intuitive platform for creating automated workflows. It enables users to build and customize flows through a visual interface, accessible to both technical and non-technical users, thus automating repetitive tasks, enforcing business rules, and streamlining processes within the Salesforce ecosystem.

For automation that requires complex orchestration interacting with transactional data, Salesforce offers Apex as a pro-code language for writing business logic.

**Visual Logic Builder**: Customers and ISVs use the Flow Builder, a drag-and-drop interface, to create process automation flows without coding. This visual tool is user-friendly for all technical levels, allowing business analysts and administrators to easily design complex automations.

Flow Builder enables customers to create versatile flows that operate in various contexts, supported by the Core Flow Engine:

- **Record Triggers**: Flows activate upon record updates or form submissions, enabling data modifications, validations, and workflow initiations based on customer actions.
- **Scheduled or Event-Driven Flows**: These flows can operate on a predetermined schedule or trigger after specific events, and can make callouts to external services.
- **Screen Flows**: Provide a user interface for guided, step-by-step processes with forms, screens, and other interactive elements, useful for tasks like data entry, troubleshooting, or onboarding.
- **Orchestrator Flows**: Manage and integrate multiple step processes, facilitating the handling of complex operations.

The Offline Flow Engine can run without a connection to the Salesforce app server. Offline Flow powers automation for Field Service mobile use cases. The High-Scale Flow Engine powers marketing flows. It offers B2C scale for processing a high volume of long-running flows simultaneously.

All use cases and environments are enhanced by a unified metadata model in Flow Builder, which supports a variety of powerful logic elements applicable across all Process Automation flows:

- **Advanced Logic and Conditions**: Users can integrate complex logic like decision elements, loops, and wait conditions into their workflows, allowing for the handling of intricate business scenarios.
- **Data Management and Transformation**: Flow Builder enables data ingestion, transformation, and management from various sources including web services, Salesforce orgs, and Data 360. It supports comprehensive data operations such as creation, updating, deletion, and querying of records.

Salesforce Process Automation offers seamless integration with other Salesforce products and third-party systems, ensuring smooth data flow between applications for a unified view of business processes and customer interactions. It supports various integration methods such as APIs, web callouts, and MuleSoft connectors.

External Services and MuleSoft connectivity within Salesforce enables connections to external APIs and the utilization of their data within Salesforce Process Automation. Registering the API schema allows for the creation of invocable actions that integrate seamlessly into flows, facilitating the automation of processes with external data sources. MuleSoft’s robust integration capabilities ensure seamless data flow between Salesforce and other applications, eliminating data silos and providing a unified view of business processes.

**Agentforce Integration**: Salesforce Process Automation leverages Agentforce to enhance workflows with intelligent decision-making. It uses AI insights to automatically direct leads to suitable sales representatives or initiate tailored marketing campaigns based on customer behavior, thereby boosting the effectiveness of automation with added intelligence.

**Platform Synergy**: Salesforce Process Automation integrates seamlessly with other Salesforce products like Sales Cloud, Service Cloud, Commerce Cloud, and Marketing Cloud. This integration enables organizations to automate processes across various departments, enhancing operational efficiency. For instance, a workflow can automatically generate a support case in Service Cloud when a customer complaint is submitted via a Marketing Cloud form.

Apex is a powerful, object-oriented programming language that allows developers to write custom business logic and perform complex operations on the Salesforce platform. It has been a mainstay of our platform, and currently the platform handles over 350 billion Apex transactions per month (as of October 2025).

Apex is used to develop a wide range of custom functionalities and deep integrations into the Salesforce platform, including:

- **Trigger-Based Automation**: Implement complex automation that executes before or after records are inserted, updated, or deleted. This allows for intricate data validation, related record updates, and the invocation of other processes based on specific data changes.
- **Web Services:** Create custom integrations with external systems and call REST or SOAP APIs from Apex.
- **Custom User Interfaces**: Build highly customized user interfaces and experiences using Visualforce and Lightning Web Components (LWC), where Apex serves as the backend controller to handle data manipulation and business logic.
- **Custom APIs:** Developers can expose custom logic as APIs using Apex REST and Apex SOAP, enabling external systems to interact with Salesforce data and processes programmatically.
- **Async processing**: Run long-running or resource-intensive tasks asynchronously through future methods, Queueable Apex, and Scheduled Apex. This allows long-running operations to be offloaded and processed in the background, improving user experience and system performance.
- **Scheduled Apex:** Developers can schedule Apex classes to run at specific times using the Apex Scheduler for periodic tasks like nightly data synchronization, report generation, and maintenance activities.

The User Experiences capabilities on the Salesforce Platform enable end-users to interact with applications through various deployment options across browser-based Lightning Applications, Experience Sites, mobile-native, AI-oriented, collaborative UX, or embedded components using Lightning Out.

The Salesforce Lightning Design System (SLDS) is a comprehensive design framework that fosters the creation of consistent and accessible user interfaces with Salesforce’s design principles for a cohesive user experience across all products. It empowers Salesforce engineers, customers, and partners to build applications that feel native across the Salesforce ecosystem.

The key features of the design system include:

- **Design Patterns**: Proven solutions to common design challenges, providing guidelines for layout, data presentation, and user interactions to ensure a consistent user experience.
- **Styling Hooks**: CSS variables that represent design decisions, such as colors, typography, spacing, and sizes, ensuring consistency across applications.
- **Lightning Base Component Library**: A collection of reusable UI components, like buttons, form elements, and navigation elements, that adhere to Salesforce’s design principles, facilitating quick and efficient development.
- **Accessibility**: Built-in accessibility features and guidelines to ensure that all components are usable by individuals with disabilities and adhere to standards, like Web Content Accessibility Guidelines (WCAG).
- **Responsive Layouts**: A flexible grid system and layout guidelines that allow applications to adapt seamlessly across different devices and screen sizes.
- **Tooling**: A collection of tools, resources, and technologies that support component hygiene, anti-pattern reduction, and design system governance.

The SLDS framework continues to evolve to support richer styling hooks and deeper customization capabilities so that components can be reused while still being customized to meet unique branding and theming requirements. Our design system aspiration is to make Salesforce fast, easy, and compelling to use with AI.

Salesforce’s browser-based interface, known as Lightning, offers a consistent UI container and a metadata-driven UI framework and collection of technologies for Salesforce engineers, IT admins, developers, and partners to rapidly develop UI with a consistent Salesforce aesthetic, as well as extension points for complete control to re-style and re-brand. The Lightning Web Stack includes several technologies:

- **Lightning Web Components**: Custom web components built with HTML and JavaScript, adhering to W3C web standards.
- **Lightning Web Security**: A virtualization engine that manages JavaScript code in the browser, ensuring compliance with Salesforce’s security standards for third-party code.
- **Lightning Data Services**: A framework designed for efficient interaction with server-side data.
- **Lightning Web Runtime**: Ensures performant and consistent UI rendering across various clients.

Salesforce engineering has incorporated lessons from previous UI technologies and contributed to web standards bodies, influencing the development of standards-based component implementations. For example, Salesforce continues to be a member of approximately 20 W3C working groups. The Lightning Web Components and Lightning Web Stack align with these industry standards, reducing complexity for developers.

Mobile continues to be a growing and critical interface for users to interact with Salesforce apps.  
Salesforce provides a native mobile app so all browser-based Lightning apps can become mobile apps without having to write new code. Salesforce also offers a spectrum of tools, SDKs, and capabilities for creating fully custom native apps optimized for devices. These include:

- **Mobile SDK**: Pro-code interface for developers across mobile operating systems that simplifies integration with authentication, session/token management, Salesforce APIs, and much more.
- **Mobile Native Runtime**: Enables developers to create metadata-driven native experiences dynamically rendered at runtime using iOS and Android technologies that also leverage on-device capabilities.
- **Branding**: Allows customization of mobile app aesthetics through the Mobile Publisher Pipeline for converting Salesforce mobile apps into customer-branded apps.
- **Offline Capabilities**: Ensures seamless app functionality with inconsistent or no internet connectivity.

Mobile Customization Framework (MCF) significantly enhances the development of native Salesforce mobile applications by offering ease of use and extensive customization options. Key advantages include:

- **Metadata-driven approach**: MCF utilizes metadata, which can be sourced from visual builders, common repositories, and Salesforce-hosted resources, to create dynamic and adaptable user experiences tailored to specific needs.
- **Experimentation and optimization**: The framework supports runtime experimentation with different layouts, facilitating ongoing engagement optimization and user experience refinement.
- **Extensibility**: Designed for flexibility, MCF allows integration of custom components into the core metadata framework, enhancing functionality and versatility.
- **Composable user experiences**: Utilizing the latest iOS and Android technologies, MCF supports the assembly of reusable components like buttons, lists, and cards to craft sophisticated user interfaces.
- **Runtime customization**: MCF enables real-time UI customization and experimentation, fostering a more personalized and engaging user experience.

Offline and low-connectivity scenarios are an increased concern when using apps on mobile devices. The mobile technology stack prioritizes building apps that can be offline-first. Key features include:

- **Cache First Experience**: Focuses on caching data for offline use, ensuring high performance and security. User interaction is also designed with offline-rendering principles in mind.
- **Cache Management**: Keeps the cache relevant and updated, even when offline.
- **Shared Cache**: Utilizes a single cache for both native and hybrid screens, facilitating seamless offline experiences.

Nimbus is the platform’s production-ready solution that simplifies the process of accessing device capabilities for hybrid app developers. Traditionally, bridging the gap between JavaScript and mobile native code was a complex task. However, with Nimbus, developers can now harness the full potential of mobile devices without delving into low-level coding. Key features include:

- **Broad Access**: Provides seamless integration with a variety of device features like camera, microphone, geolocation, and LiDAR.
- **Standardized Interface**: Offers a uniform method for accessing device capabilities.
- **Hybrid App Integration**: Enables hybrid apps to fully utilize device functions.
- **Efficient Development**: Streamlines the app development process, reducing complexity.

As AI continues to transform what’s possible with Salesforce apps, Salesforce also provides a differentiated user experience by leveraging on-device, task-specific AI models alongside cloud-based solutions:

- **Small Language Models (SLM):** These can run on mobile devices efficiently and at a lower cost.
- **Privacy and Security:** Ensures user privacy and maintains trust and security at levels comparable to server-based models.
- **Offline Functionality:** Operates effectively in low-connectivity environments, enabling offline use cases.
- **Voice:** State-of-the-art speech-to-text, natural text-to-speech, and speaker diarization models now run natively on devices, delivering high-fidelity voice interactions with full privacy and zero latency.

Non-model UI for natural language and multi-turn interactions with our app will continue to grow in prevalence. Future developments are expected to enhance integration between models, device capabilities, and applications, improving user interactions through more intuitive voice and text interfaces. On-device metric collection will also allow for personalized adjustments based on user preferences.

Collaboration is essential among all users, including both humans and agents, to harness the combined strengths of automation and human supervision. This collaboration is particularly crucial for complex business interactions involving an organization’s employees and its customers. Slack serves as a primary tool within the Salesforce Platform, facilitating this interaction through direct messaging and multi-user channels tailored to specific discussion topics. These discussions can range from spontaneous, user-created conversations to more structured dialogues centered around specific data within a user’s workflow, such as a detailed Slack message thread addressing a significant customer issue.

Looking forward, the Salesforce Platform plans to enhance the collaborative experience currently provided by Slack. This expansion will aim to fully utilize the extensive capabilities of the platform, enriching the way users interact and collaborate within the digital workspace.

The Developer Experience capabilities on the platform provide tools for building, customizing, testing, and deploying apps, focusing on the spectrum of low-code through pro-code approaches, ensuring equal opportunities for developers of all skill levels.

- **Low-Code Tools**: These include Schema Builder for data models, Flow for business rules, and AppBuilder for UI customization, all designed to simplify the development process by manipulating structured metadata and work in the language of the business solution, instead of technical concepts and jargon.
- **Pro-Code Tools**: For developers needing richer and complex customization, the platform offers tools like Salesforce Code Builder, a cloud-based IDE, along with a Command-Line Interface (CLI) and APIs for advanced coding and component creation. Developers can code in the language of their choice by leveraging solutions for deploying, managing, and optimizing apps with Heroku.
- **Integrated Development Environment**: The Salesforce ecosystem supports seamless integration between low-code and pro-code tools, as well as coherently developing in-cloud and locally with industry-standard tools.
- **Application Lifecycle Management (ALM)**: Features a range of sandbox orgs for development separate from the production environment, including scratch orgs for initial development and full sandbox orgs for testing against production-like data and scale.

AI and “Developer Assistants” are revolutionizing the developer experience by simplifying and accelerating the creation of efficient, high-quality applications. At Salesforce, our AI Research and Developer Experience teams are continuously iterating and exploring how predictive and generative AI with agentic reasoning, can be transformed into powerful developer agents. These developer agents are natively integrated with tools developers already use, like VS Code, Code Builder, command line, DevOps Center, and Code Analyzer, making them more relevant and impactful.

We’ve made significant advancements in code analysis to identify anti-patterns and hotspots in Apex code, and then provide critical recommendations to improve their implementation. The identified issues usually waste computing resources and often lead to incidents at a high-scale. This was launched as ApexGuru Insights in January of 2024.

In the first year following its launch, over 2,800 Salesforce orgs used ApexGuru to analyze and improve their Salesforce implementation. More than 22,000 recommendations were successfully implemented, leading to a savings of 28,000 CPU hours each week. This enhancement not only boosts performance but also contributes to environmental sustainability by reducing CO2 emissions by 135 kg weekly, aligning with our core value of Sustainability and commitment to lower carbon emissions.

We are also integrating AI into pro-code developer tools and capabilities to improve developer productivity. Productized as “Agentforce for Developers” in 2024, developers can access these new capabilities within the Salesforce Extension packs in Visual Studio code and Code Builder. These extensions enable:

- Inline code suggestions as the developer writes and code generation for Apex and Lightning Web Components (JavaScript, CSS, HTML).
- Code explanation and documentation generation for Apex and Lightning Web Components.
- Apex unit test code generation.
- A distinct multi-turn chat experience in the IDE that can work on multiple responses for code generation, explanation, and documentation.
- Lighting Web Components optimizations.
- Agent Generation with human-readable YAML metadata, inclusive of Agent testing and debugging capabilities.

As of October 2025, over 42,000 developers are actively using this technology monthly, with 17.6 million lines of code accepted. This comprehensive suite ensures a flexible, integrated, and efficient development environment, catering to a wide spectrum of development needs within the Salesforce Platform. AI developer tools are also enhanced with an architecture that works across multiple external and Salesforce-built models to choose the most effective and efficient model for a given use case.

The Model Context Protocol (MCP) is an emerging open standard designed to allow AI agents to securely and consistently interact with any tool or data source. Salesforce is natively integrating MCP support into the Salesforce developer toolkit to help developers agents that can access capabilities and tools across their enterprise. This includes:

- **Local MCP Server:** A local MCP server allows developers to easily build, test, and debug their agentic integrations within their local IDE before deploying to production, dramatically improving productivity. The local MCP server offers specialized tools for org interactions and development workflows, such as mobile development, accessibility testing, Aura-to-LWC migration, and agentic DevOps. The local MCP server also includes integration with agentic reasoning and LLMs to better empower developers to “vibe code” their app iteratively and in natural language.
- **Custom MCP Server for Salesforce APIs:** Developers can now securely expose Salesforce APIs, Data 360 objects, and automation Flows as MCP "tools". This turns the entire Salesforce Platform into a rich, trusted, and discoverable set of capabilities for any external AI agent or application, complete with granular access control and the potential for new consumption-based monetization models.
- **Native External MCP Connectivity:** Developers can also securely manage connectivity to external servers that comply with the MCP standard. This enables developers to build agents that can work across their enterprise.

Our application clouds, including Sales Cloud, Service Cloud, Marketing Cloud, Revenue Cloud, and Commerce Cloud, are built on the Salesforce Platform, offering leading business capabilities and composing our Application Suite to drive Customer Success. Key features include:

- **Seamless Integration**: Deeply integrated, and designed to work cohesively across the customer journey and ensure smooth data and process flow across customer touchpoints, enhancing the customer experience.
- **End-to-end Customizability**: Built on our platform, our applications offer extensive customization options from no-code to pro-code, allowing precise tailoring to customer needs.
- **Advanced AI Capabilities**: Deliver agent-assisted and agent-autonomous interactive channel based workflows with our Agentforce Agents. Incorporates predictive and generative AI to boost efficiency through automation, predictive analytics, and personalized user experiences, providing actionable insights and recommendations.
- **Real-Time Data Processing**: Utilizes Data 360 for real-time data access and analysis, supporting timely and informed decision-making based on the most current information. This enhances responsiveness and agility in fast-paced environments.
- **Unified Data and Analytics**: Integrates various data sources into a centralized platform for consistent and comprehensive data views, delivering accurate analytics and improving decision-making.
- **Enhanced Security and Compliance**: Features robust security and compliance tools to protect sensitive data and meet regulatory standards.
- **Consumer-Grade User Experience**: Offers intuitive, user-friendly interfaces that make applications accessible and effective across devices, channels, and modalities.
- **Reliability**: Ensures minimal downtime and scalability to support mission and life-critical operations, including emergency services and critical transportation systems.
- **Elastic Scalability**: Built on Hyperforce that supports increasing data and user interaction volumes without sacrificing performance or cost to serve.
- **Continuous Improvement**: Regularly integrates innovations to enhance capabilities without disrupting existing operations.

Salesforce is dedicated to advancing its applications by unifying capabilities across its platform, building on the foundational technologies described in this white paper. This transformation is guided by a set of key priorities that shape the design and development of Salesforce’s application suite.

Our application teams specialize in performance and scalability, utilizing advanced performance labs to create exact replicas of our production environments with synthetic data. This setup allows for extensive simulation of parallel user journeys to ensure each new feature is thoroughly performance tested and its impact assessed. When runtime bottlenecks are identified, we dynamically adjust rate limits and other measures to protect system health while also gathering data to drive resolution.

Our systems are designed for horizontal scaling to utilize the flexibility of the public cloud effectively. Automated checks ensure that updates or enhancements don’t adversely affect performance. We employ predictive autoscalers that proactively manage system load, not just reacting to increased demand but anticipating and adjusting beforehand.

Autoscaling is crucial for minimizing ‌cost to serve by reducing unused capacity. We monitor system running costs closely, identifying and addressing any inefficiencies in auto-scaling or resource use. While cost efficiency is important, we prioritize reliable application delivery, opting for autoscalers that scale up quickly and down slowly to maintain customer trust, even if it incurs higher costs.

Data models are fundamental to all business operations at Salesforce, influencing Business Capabilities, APIs, navigation, UI displays, and the reports that can be created. They’re integral to the platform’s functionality.

Our application suite shares a common data model across Sales Cloud, Service Cloud, Revenue Cloud, Commerce Cloud, Marketing Cloud, and Industries Cloud. This contributes to our integrated suite, providing consistent behavior and interoperability, and clear paths for upgrades and extensions.

For example, the sharing of Account and Product entities across all Clouds allows users in both Marketing Cloud and Sales Cloud to exchange data, metadata, UI components, and business logic. This integration helps break down silos and fosters cross-functional collaboration.

A common data model across all Salesforce Clouds significantly enhances integration but may not meet all complex partner integration needs. The Data 360 Common Data Model expands on this by extending the shared data model benefits beyond Salesforce’s typical data boundaries, accommodating more extensive integration scenarios.

Salesforce’s Metadata Framework allows various groups like engineering teams, ISVs, partners, admins, and end-users to customize and expand their applications within distinct layers of extensibility without interfering with each other. This structure supports a scalable environment where modifications by one group don’t disrupt others, maintaining system integrity.

A prime example of the Framework in action is the Unified Knowledge product, which integrates all knowledge sources into a data lake. This setup includes a semantic layer and retrievers, enhancing predictive and generative AI capabilities across Sales Cloud, Service Cloud, Revenue Cloud, Marketing Cloud, and Commerce Cloud. It incorporates a data model for unstructured and semi-structured knowledge linked to the existing structured knowledge model.

Additionally, the Framework uses metadata to define custom relationships between data types, facilitating advanced query generation. This allows application teams to create customizable applications that leverage this comprehensive knowledge base, while ISVs, partners, and customers can further enhance application capabilities by modifying metadata relationships or developing custom retrievers for specific business use cases.

Customer data is securely stored across various platforms like SalesforceDB and Data 360, and is standardized and normalized regardless of its structured or unstructured format. This ensures consistent data handling through a unified format known as the sObject, which supports a cohesive data platform across all customer data.

This standardization enables a single API for all data operations, a unified interface for triggers in Apex, and custom workflow creation with Flow. It also supports Tableau Next, allowing for customized data views and integration with generative AI tools like Prompt Builder for intelligent response generation based on customer data.

Additionally, Salesforce applications integrate with various data stores to enhance business process flexibility within products. For example, in Marketing Cloud, Flow is used to manage multi-touch customer experiences, with options to use pre-designed templates or build custom Flows that integrate marketing with other business processes, all based on underlying customer data.

Applications leverage and enhance shared services such as identity resolution, content orchestration, personalization, analytics, LLM Gateway, and Reasoning Services, enabling rapid innovation and delivery. These services support real-time data processing, AI-driven insights, and enriched user experiences, providing a comprehensive 360-degree customer view.

Benefits include improved efficiency through intelligent automation and predictive analytics, scalability for increasing data and user interactions, and robust security and compliance. The platform’s customization capabilities allow organizations to quickly adapt to changing needs, fostering growth and operational excellence.

Innovation at the Application Tier is propelled by the Salesforce Platform and individual applications, enhancing the Salesforce ecosystem and establishing applications as industry leaders.

Salesforce applications are designed to meet users across a variety of platforms, including web, mobile, email, SMS, WhatsApp, and other channels. They optimize ‌each channel’s native capabilities to enhance user experience and efficiency.

Features include multi-month offline capabilities for Salesforce Field Service users, browser push notifications, and wide-screen layouts for service agents in Lightning Service Console, and high-performance storefronts and co-pilots for Commerce shoppers.

The metadata platform ensures that Salesforce, its partners, and customers can immediately benefit from these capabilities right out of the box.

Salesforce’s Foundation Services, Platform, and Shared Business Capabilities allow applications to quickly adapt to market shifts and technological trends, enabling rapid innovation delivery. For instance, with the advent of generative AI, Salesforce swiftly utilized existing AI services like the NLP Trust Layer and Intent Detection to incorporate prompt templates into the Universal Communications Platform. This integration enhances messaging and phone functionality across products, facilitating more personal client connections.

Following the trend towards autonomous AI, Salesforce launched Agentforce, a solution that capitalizes on these existing investments to automate business use cases with agents efficiently, without the need for building from scratch.

We’ve rebuilt Marketing Cloud, Revenue Cloud, and Commerce Cloud on the Salesforce Platform, enabling these Clouds to share the same infrastructure, platform, metadata, data, AI, UI components, and business logic, while benefiting from the full power of the Salesforce Platform. For example, we have taken features from Revenue Cloud and embedded core capabilities such as the constraints-based configurator, pricing engines, and catalog management, making them foundational services that are available across the suite. This also enables us to have seamless integration across all of our clouds, and the capabilities that Commerce Cloud and Marketing Cloud deliver become part of the shared business capabilities that can be leveraged by the other applications. This is our integrated application suite vision delivered.

The Salesforce Platform’s journey has led to the development of an integrated application suite that combines Sales Cloud, Service Cloud, Marketing Cloud, Revenue Cloud, and Commerce Cloud into a unified solution. Available from the Salesforce Starter Edition onwards, this suite offers multi-channel outreach, customer relationship management, and business insights in one cohesive package. Regardless of the edition chosen, users can access the core capabilities of Sales Cloud, Service Cloud, Marketing Cloud, and Commerce Cloud, ensuring a consistent experience across all levels.

Salesforce Industries products for Financial Services, Health, Life Sciences, Media, Energy and Utilities, Manufacturing, Auto, Consumer Goods, Retail, Net Zero, Public Sector, Education, and Nonprofit, extend our application products and platform to provide tailored solutions that address industries’ unique challenges. They streamline operations and enhance productivity by incorporating industry-specific workflows, compliance measures, and data models.

The Industries portfolio has been rebuilt on the Salesforce Platform to enable composability across verticals. Customers can now assemble one or more industry capabilities into tailored solutions, leveraging shared metadata, APIs, and business services. This approach balances vertical differentiation with platform consistency, ensuring adaptability and scale across diverse regulatory and business contexts.

Our products utilize a layered architecture. At the base is the Salesforce Platform and horizontal applications such as Sales Cloud and Service Cloud, serving as the foundation for all industry solutions. To this, Salesforce has added value-added common services that enhance reusable components that are embedded across most Industries. Examples of these include capabilities for Digital Automation, Timelines, Action Plans, and more. Above this layer, there’s a reusable business logic layer that encapsulates horizontal capabilities such as feedback management, CPQ (config, price, quote), and service management.

The top layer features domain-specific customizations tailored to meet specific industry requirements, leveraging the underlying platform for enhanced scalability and efficiency. For example, in the manufacturing vertical, this setup optimizes production planning through accurate forecasting. In the life sciences sector, it provides pharma sales teams with mobile offline solutions that efficiently manage workflows and sample handling while complying with various geographic regulatory requirements.

**Trusted AI Excellence**: Our trusted generative AI solutions provide industry-specific AI capabilities. These include agents and prompt engineering, which facilitate low-code/no-code automation and digitization in sectors such as healthcare, life sciences, and financial services. Additionally, features like document/text mining and summarization cater to industries handling large volumes of data, aiding in information extraction and insights gathering.

Customized agents enhance three-way communication between agents and customers, leading to quicker resolutions. The trust layer of the Salesforce Platform facilitates adherence to all compliance and regulatory standards across industries.

**Data, Insights, and Intelligence with Regulatory Compliance and Security**: Salesforce Industries offers a comprehensive 360º view with stringent data privacy, sharing, and security measures tailored to specific industry regulations like GDPR, HIPAA, and FedRamp. Salesforce integrates data from various sources, enabling compliance and security, and enhances these solutions with additional features like Shield Encryption BYOK (Bring Your Own Keys) for tenant data encryption.

**Elevated User Experience**: Salesforce Industries emphasizes a seamless user experience that is tailored to industry-specific needs to enhance the user journey. This includes tools like the Actionable Resource Center, Experience Cloud templates, and OmniStudio-based solutions.

**Digitization, Integration, and Onboarding**: Salesforce Industries provides digitization, integration, and onboarding through low-code to no-code solutions, leveraging tools like Flows and Omnistudio for new customers and offering migration solutions for existing CRM systems. Integration with external systems and data is streamlined via the connectors offered by MuleSoft. Salesforce also includes industry-specific service processes, such as dispute management for retail banking.

**Mobile and Offline**: Salesforce Industries provides robust domain-specific support for the Salesforce Mobile App and Field Service Mobile App. For highly specialized domains requiring advanced offline support, Industries provides bespoke Mobile Apps built on Salesforce Mobile SDKs.

**Common Business Capabilities**: Salesforce Industries builds on a foundation of common business capabilities, enabling consistency and productivity while tailoring solutions to unique industry needs, such as different appointment booking systems for banks and hospitals. Integrated with the broader Salesforce ecosystem, Salesforce provides a holistic Customer 360 view, making it a vital part of the Salesforce product suite.

For years, the Analytics and Business Intelligence (BI) platform market has promoted visual self-service and AI-driven automated insights for end users to help them make quicker, more data-driven decisions. However, we know not everyone has seen this come to fruition due to several challenges:

- **Disconnected Insights**: Insights aren’t integrated into users' workflows, making it difficult to take action on the insights, despite their potential to inform decision-making.
- **Data Overload and Silos**: Data continues to grow rapidly and remains compartmentalized, leading to disorganization and security risks. Organizations face a dilemma between a chaotic, self-service data environment and a restrictive, well-governed data environment.
- **Distrust in Data**: The expansion and fragmentation of data has eroded users' trust in the insights derived from company data.
- **Lack of Composability**: There’s a significant absence of composability and reuse in work processes, forcing users to repeat tasks and without clear avenues for monetization.

Tableau Next is designed to broaden the cycle of visual analytics by bringing together business users and data professionals in new, collaborative ways; all augmented with AI. It provides timely, trusted metrics and insights via the Salesforce Platform, facilitating ubiquitous access to actionable insights.  
![Analytics](https://a.sfdcstatic.com/developer-website/prod/images/architect/analytics-tableau-next-data.png)

Tableau Next addresses these challenges by:

- Creating an open, composable, API-first platform for connected experiences from data connection to action. Providing tools for development, composable components for rich analytical applications, and capabilities to manage their packaging and distribution.
- Building with AI at the core, and able to provide contextual and relevant insights, with tools for data professionals to efficiently review and validate to ensure trust.
- Building on Tableau Semantics as a universal semantic layer for quick, self-service, and governed data analysis within a controlled yet flexible ecosystem.
- Offering real-time, cloud-scale data capabilities through Data 360 for trusted, scalable, and governed data access.
- Providing a rich environment and marketplace for developers to build and monetize applications.
- Integrating intelligence at its core, bringing the power of your organization’s semantics and knowledge to the agents that empower you.
- Prioritizing trust, so you can have confidence in your data, analytics, and agentic workloads and deployment, through direct control and visibility into their activities and efficacy.
- Leveraging collaboration as a first-class design principle, with deep and rich integrations with Slack, as well as any other collaborative tool for your organization.

Tableau Next builds on Tableau’s leadership in data analysis tools by offering an open platform that enhances capabilities and integrates experiences. Key features include:

- **Rich Data Visualization**: Utilizes Tableau’s VizQL technology for expansive visual analytics.
- **Collaborative, Governed Workspaces**: Offers a unified interface for analytics tasks, integrates with Slack for real-time collaboration.
- **Trusted, Governed Data**: Supports self-service analysis with structured promotion paths for global management in a secure environment.
- **Advanced Metric Authoring**: Enables analysts to create and reuse KPIs efficiently across your organization, facilitating consistency and reliability.

Tableau Next is fundamentally built with Agentforce as a foundational architectural construct, enhancing Tableau Next’s ability to deliver highly connected, trusted, and collaborative AI-powered data tools.

- **BI Tools**: Improves efficiency in self-service analysis for data workers, focusing on data preparation, and the curation of visual and semantic metadata.
- **Contextual Experiences**: Brings data insights, experiences, and transparent AI into the context of where most of an organization works (e.g. Slack).
- **Agentforce Architecture**: Built on the Agentforce stack, providing Tableau Next with rich context on an advanced agentic architecture.
- **Semantic Catalog**: Offers a centralized system for managing metadata, lineage, and search, enabling shared experiences across Tableau Next users.
- **Shared and Generated Metadata**: Facilitates seamless workflows between self-service analytics and governed content within a comprehensive ecosystem.
- **Action Framework**: Takes insight to action through pre-packaged, human-curated, or generated workflows.
- **Personalized Insights**. Learns your data preferences, your role, and much more (to the degree you allow it to), to bring highly contextualized and personalized data insights to you immediately.
- **Proactive Insights**. Intelligently explores your data ecosystem, looking for places of statistical interest for you; while proactively understanding the drivers of the change, what to do about it, and recommends actions to take as next steps.
- **Trusted Data Agents**. Gives the power back to you, as the driver of your data agents, to build and tune the application through integrated experiences. It also gives you testing tools to pre-evaluate your data changes and their impact on the accuracy and efficacy of your agents.

Tableau Next enhances business user experiences across various platforms like Slack and Salesforce, and through new analytics features like Tableau Pulse, all accessible via agentic experiences to simplify analytics engagement. Key aspects include:

- **Collaboration**: Central to trusted analytics, it facilitates interaction across different analytical components and integrates validation tools within users' workflow.
- **Pulse Metrics**: Delivers both curated and automated insights more efficiently than traditional analyst-created dashboards.
- **AI-Driven Experiences**: Employs AI to reduce the need for technical expertise in advanced analytics, helping to ensure reliability with deterministic metadata and governed data.
- **Multi-Player Insight Delvery**: Allowing business users to work collaboratively with analysts to gain knowledge and trust in the insights the system delivers.
- **Deep Integration**: Built on a shared metadata and data platform, giving composability across different systems and experiences to allow for composability for promotion, data flow, and for different personas helping one another to review and complete work.

The Tableau Semantic Layer serves as a crucial bridge between raw data and user interpretation, simplifying data analysis, decision-making, and application development, and enhancing AI-driven context and retrieval. Key features include:

- **Integrated Metadata Management**: Supports both self-service and governed metadata, facilitating ad-hoc analysis with structured pathways to becoming the organizational single source of truth.
- **Tableau’s Best-of-Breed Capabilities**: Including multi-logical-object support, model composability, shared dimensions, complex geospatial hierarchy, and temporal modeling.
- **Diverse Data and Analytics**: Assists in linking unstructured and structured data, such as correlating image-based product categories with structured sales data, and incorporating sentiment analysis from semi-structured product reviews.
- **Salesforce Platform Integration**: Establishes a unified source of truth, facilitating consistent business semantics and seamless integration across applications and a cohesive metadata model that supports various user experiences and use cases.
- **Agentic Intelligence**: The semantic layer is one of the key areas where agents gain ‌ intelligence by understanding not just the data and metadata that power your business, but also the semantics that define it, including deeper descriptions and preferences that are bespoke to your organization.

Tableau Next offers integrated solutions that enhance data-driven decision-making and trusted automation, featuring simple actions, predefined Flows, scheduling, and API integrations. Key components include:

- **Standardized, Intelligent Business Actions**: Facilitates urgent and context-specific communications within businesses, which are essential yet complex.
- **Pre-defined and Generated Flow Schedules**: Enables both ad-hoc and scheduled actions through static and dynamically generated flows that are trustworthy yet verifiable.
- **Agentforce**: Supports AI-driven data conversations and interactions, allowing users to engage with insights and perform actions similar to those in a traditional UI, both within and outside their business applications, and simplified through conversation.

Tableau Next offers a composable developer platform with no-code, low-code, and pro-code options for application development, all utilizing Tableau Semantics on Data 360. Key offerings include:

- **Pre-packaged Industry/Intelligent Applications**: Provides templated and customizable analytical applications tailored to specific industry needs.
- **3rd Party and ISV Applications**: Supports the creation of dynamic and interactive applications for analytical, industry-specific, and custom purposes.
- **Market and Exchange**: Allows ISVs and developers to package and distribute their applications within the largest and most trusted business application development ecosystem.

Tableau Next is designed for both business users and data professionals, fostering a collaborative approach to data understanding. Whether technical or non-technical, all team members, from business users to data experts, can review each other's data insights. Moreover, these insights are not limited to a browser tab within a BI platform.

As a BI platform, Tableau Next is:

- **Composable across platforms**. Insights are rendered in the same way, regardless of the platform you view them on. This consistency is a pillar design principle when working with data visually.
- **Deeply integrated with Slack**. Integration development with Slack has ensured one of the most intuitive and immersive collaborative data experiences on the market today.
- **Open for any tool**. The application of our API-first principle, on our deeply unified platform, ensures that integration can extend to other collaboration and third-party tools, retaining the richness throughout.

While the Salesforce Platform offers a comprehensive suite of integration capabilities to address a broad range of digital challenges, many customers operate within enterprise architectures that have developed over time through the use of various vendors and technologies.

Modern enterprises face challenges with system integration and business process automation, often resulting in data silos and inefficiencies. The Salesforce Integration Platform, leveraging the power of MuleSoft, tackles these issues by facilitating the rapid development and enhancement of automated processes. It ensures seamless system connectivity, enhances information flow, and supports decision-making across different platforms, thereby reducing labor costs and automation expenses. This layer is crucial for creating, managing, governing and monitoring integrations between Salesforce services and other custom or third-party services.

Systems are defined through APIs, which serve to:

- Access data from essential systems like ERP, customer and billing systems, and proprietary databases.
- Facilitate data interaction and integration, helping to eliminate data silos.
- Add business context to the data and processes managed by System and Process APIs.

For effective communication, APIs are described using:

- OpenAPI Specification (OAS) for immediate synchronous exchanges
- AsyncAPI for asynchronous, event-driven communications
- Model Context Protocol (MCP) for structured, model-context interactions
- Agent-to-Agent (A2A) protocol for direct agent-to-agent integrations.

The Salesforce Integration Layer provides robust capabilities to integrate and manage any system, enhancing connectivity with Salesforce's data, AI, and app functionalities, regardless of whether the systems are native to Salesforce or from other providers.

Complex integrations require advanced transformations and need robust tools, including universal connectivity; API management & governance; an integrated development environment (IDE) for building integration workloads; a runtime platform to deploy, manage, and oversee these integrations; and an observability platform to provide end-to-end visibility into these integrations.

To further expedite the integration process, we offer accelerators and industry-specific templates that encode common integration patterns and needs.

Two primary integration patterns address the flow of data and processes between Salesforce and the broader ecosystem: outbound integration and inbound integration.

**Connecting Salesforce to External Systems (Outbound):** This pattern involves processes originating from within Salesforce that access data or trigger actions in external systems.

- **Secure Endpoint Management (Named Credentials):** Named Credentials provide a secure, centralized location to store endpoint and authentication details. Applications and automations reference a logical name, while the platform handles the complexities of the authentication lifecycle.
- **Declarative Integration (External Services):** For external systems that offer a standard OpenAPI Specification, an administrator can use External Services to register the API declaratively. The platform then processes the specification, making the service’s operations automatically available as native actions in tools like Flow or as native objects in Apex.
- **Complex System Integration (MuleSoft)**: For systems lacking modern interfaces, MuleSoft creates a standard, reusable API layer. This abstracts away legacy complexity and brings on-premises data and processes into the Salesforce ecosystem.
- **Real-Time Data Access (External Objects):** Represents tables from external systems as virtual objects within the Salesforce data model, making external data accessible via standard queries and UI components without replication.
- **Central Capability Management (Unified API Catalog):** The Unified API Catalog is a centralized repository and the single source of truth for all API specifications and their associated metadata, such as their location and security protocols. It ensures that no matter where a piece of data or business logic resides, it can be discovered, securely connected to, and composed into powerful new applications and automations across the Salesforce ecosystem.
- **Custom Pro-Code Logic (Apex REST):** Developers can expose custom business logic written in Apex as a REST API and action. The action is then available as a step in a Flow, or a tool for an AI agent.

**Connecting External Systems to Salesforce (Inbound):** This pattern enables external systems and applications to connect to the Salesforce Platform to access data, trigger business logic, and orchestrate processes. This capability is built upon a foundation of proven, enterprise-grade APIs that operate at massive scale. As of October 2025:

- The Query API (SOQL) handles over 50 billion requests daily.
- The REST API serves nearly 5 billion calls a day from external systems, with usage growing 30% year-over-year.
- The Bulk API processes hundreds of billions of records for large-scale data operations daily.

This proven reliability and scale underpins the following capabilities:

- **A Unified API Experience:** Access to all Salesforce capabilities is being unified through a consistent endpoint structure (api.salesforce.com), eliminating the need for developers to learn different patterns or authentication flows for each product.
- **A Comprehensive, Purpose-Built API Portfolio:** The platform provides a diverse collection of APIs tailored to specific needs, including REST and SOAP APIs for transactional operations, the Bulk API for large-volume data processing, the Pub/Sub API for event-driven applications, and specialized product or custom Apex APIs.
- **Future-Readiness for Agentic Integration:** Through standards like MCP, customers can securely expose their Salesforce data and actions as "tools" for external AI agents, turning a Salesforce instance into an extensible set of skills for a digital workforce.

Beyond the established inbound and outbound patterns for data and process integration, a new pattern is emerging for the agentic era. The Salesforce Platform is implementing a comprehensive MCP strategy, positioning it as both a consumer and a provider of AI-powered services. This bidirectional approach enables agentic interoperability, allowing enterprises to seamlessly integrate Salesforce data and capabilities with the evolving ecosystem of AI agents and tools while maintaining enterprise-grade security and governance.

**Salesforce as an MCP Client:** Agents can act as an MCP client by intelligently and dynamically leverage external systems and APIs. This capability enables organizations to extend Agentforce's reach beyond Salesforce boundaries, orchestrating actions across any system, whether it has a modern API or requires connection via MuleSoft to legacy systems or RPA bots. Configuration is handled through a familiar declarative, topic-based setup experience, enabling rapid integration without custom development. A simplified discovery mechanism for partner-provided MCP servers further streamlines the integration of external capabilities. By abstracting the complexities of external connectivity through a high-scale stack, enterprises can rapidly integrate Agentforce with their broader technology landscape.

**Salesforce as an MCP Server:** As an MCP Server, the platform exposes its logic and assets, including standard REST APIs, custom endpoints, Invocable Actions, and Flows, as discoverable "tools" for external agents. Through a declarative interface, customers and ISVs can create and configure their own custom MCP servers, curating capabilities into collections of tools tailored for unique business processes. This extends to MCP Prompts, creating natural synergies with the platform's Prompt Template capabilities and allowing organizations to make their investment in prompt engineering accessible to any external AI system.

This capability is governed by a multi-layered security model:

- **Application Control:** The External Client App construct provides administrators with robust control over which external agent applications can access their Salesforce organization.
- **Scoped Permissions:** Authentication is augmented by granular OAuth scoping, enabling precise tracking and enforcement of actions that an authenticated agent is permitted to perform.
- **Core Platform Authorization:** These new controls are built on top of Salesforce’s robust authorization model, including record access controls, entity and field-level permissions, and other permissions defined in Profiles and Permission Sets.

ISVs and Partners can also package and distribute MCP server configurations, enabling the rapid deployment of AI-ready integrations across the Salesforce ecosystem.

Salesforce’s modern approach to universal connectivity is *interpreted connectivity*, a metadata-centric approach for developing connectors that can be executed in any platform (MuleSoft, Flow, or Data 360) for any use case without programming. The metadata models comprehend how to connect to remote services to authenticate a request, model the data returned, create queries, page through results, and receive events (triggers) to automate a process.

For systems not using HTTP-based APIs, Salesforce offers hundreds of pre-built connectors and a complete SDK for building custom connectors. For systems without any API access, Salesforce offers Robotic Process Automation (RPA) that uses agents to automate repetitive, rule-based tasks that are typically performed by humans. These tasks can include data entry, transaction processing, and responding to simple customer service queries. To extract information from documents, Salesforce offers our Intelligent Document Processing (IDP) that leverages AI to automatically extract, classify, and process data from various types of documents, such as invoices, contracts, and forms. However information exists, Salesforce offers an automated way to retrieve and manipulate it.

With recent advancements in AI, Salesforce provides building blocks to quickly enable agentic functionality in the organization:

- **Model Context Protocol (MCP) Connector** enables organizations to quickly expose their API as MCP Tools, and make the discovery of APIs and resources easy for consumption by agents.
- **Agent to Agent (A2A) Connector** enables organizations to standardize agent-to-agent communication by providing A2A protocol support for agents. Each agent (a functional expert in the domain) can discover and delegate a customer's query to the agent best suited for the domain.
- **Inference Connector** provides building blocks to build an agent from the ground up by providing LLM calling, vector embeddings and search, RAG retrieval, and MCP tools support.

MuleSoft’s API Management, delivered via Anypoint API Manager, provides a comprehensive platform for designing, securing, governing, monitoring, and scaling APIs and microservices across any deployment environment. Organizations can manage their APIs and microservices with consistent, enterprise-grade controls and insights from a single pane of glass, regardless of the platform, with centralized management from deployment to versioning. Key capabilities include:

- **Anypoint Flex Gateway** is an application layer API gateway to manage and secure APIs, applying policies for rate limiting, caching, authentication, authorization, threat protection, monitoring, and logging at the HTTP/S level. It's a lightweight, high-performance, Envoy-based gateway designed for microservices-based distributed environments and is built to seamlessly integrate with DevOps and CI/CD workflows, while providing enterprise security and manageability across any environment while supporting both inbound and outbound policies.
- **API Alerts** let organizations define and monitor specific thresholds or conditions for their APIs to detect unusual or undesired behavior. Examples include alerts when response time exceeds a limit (for example, 60 seconds), when the number of requests in a time window is too high, when certain HTTP response codes are returned, or when policy violations occur.
- **API Analytics** gives visibility into how APIs are being used and how well they are performing. The Analytics dashboard enables organizations to track and view high-level metrics, drill down into charts, create and customize dashboards and reports to understand usage trends, policy violations, response times, request/response codes, and more.

MuleSoft Anypoint Code Builder (ACB) is our next-generation IDE designed for API and integration development, featuring a modern, unified experience with VS Code as the backend.

- **Unified Development Environment:** Consolidates the entire API and integration development process into one tool, supporting AsyncAPI, OAS, and RAML APIs, governance rulesets, a low-code Flow canvas, pre-built connectors, and integrated test and deployment options. In addition, ACB supports debugging, troubleshooting, and ongoing maintenance with intelligent, contextual suggestions.
- **Agentic Development Experience:** Delivers agentic experiences across the entire application development lifecycle. At the core is the MuleSoft MCP Server, which enables agentic Integration Development. MuleSoft MCP Server provides powerful tools for generating API specifications and integrations from natural language, creating data transformations, managing assets in MuleSoft Exchange, and administering applications and API policies. The MuleSoft MCP Server tools turbocharge users’ API specification and integration development in any VS Code based AI Code Editors, including Cursor, Windsurf, and many more.
- **AI Integrations:** MuleSoft enhances integration development with agentic capabilities utilizing MuleSoft Topic Center, which converts API calls into Agentforce Actions for enterprise system access. The Agentforce Connector embeds natural language automation into integrations. The Inference Connector securely integrates external LLM providers, enabling AI-driven logic in MuleSoft applications. Organizations can use these combined capabilities to build intelligent, adaptive integrations.

MuleSoft’s Runtime Platform provides flexible deployment options for running MuleSoft applications, APIs, and integrations across environments. Organizations can choose the runtime model that best fits their operational, compliance, and scalability needs while maintaining consistent management and governance through Anypoint Platform. This flexibility ensures that applications can run close to data sources, comply with regional regulations, and scale seamlessly based on demand.

![MuleSoft Runtime Platform](https://a.sfdcstatic.com/developer-website/prod/images/architect/runtime-platform-mulesoft-runtime-platform.png)

Key hosting options include:

- **Cloud:** MuleSoft’s fully managed, multitenant integration Platform-as-a-Service (iPaaS) that eliminates infrastructure management overhead. CloudHub 2.0 provides elastic scaling, high availability, and zero-downtime deployments/upgrades, with built-in observability needs and compliance certifications. Developers can focus on building APIs and integrations while MuleSoft manages the runtime infrastructure, ensuring enterprise-grade security, reliability, and high availability.
- **Hybrid:** For organizations that need to self-host their applications for more control, MuleSoft offers Runtime Fabric, a container service that automates the deployment and orchestration of MuleSoft runtimes across Kubernetes or virtual machines. It supports horizontal scaling, zero-downtime deployments, built-in security controls, and simplified cluster management.
- **Private Cloud Edition (PCE):** MuleSoft’s Private Cloud Edition provides a fully self-managed, on-premises version of Anypoint Platform (including Control and Runtime Planes), allowing organizations to meet strict regulatory, data residency, and security requirements. It enables large enterprises to maintain complete control over infrastructure while still benefiting from the unified integration and API management capabilities of Anypoint Platform.

MuleSoft delivers comprehensive observability solutions that provide end-to-end visibility into APIs, integrations, and applications across any deployment model. Observability capabilities are consistent regardless of where workloads run, providing a unified view of environments. By capturing both real-time and historical telemetry data, MuleSoft enables organizations to detect, analyze, and resolve production issues more quickly across the entire application network. Observability data can be viewed natively within the Anypoint Platform or can be exported via OpenTelemetry into a customer’s preferred APM, allowing seamless integration with existing monitoring ecosystems. This empowers organizations to proactively strengthen infrastructure resilience and improve the reliability of mission-critical applications.

MuleSoft provides observability through two primary offerings:

- **Anypoint Monitoring** is the current in-market observability solution built into the Anypoint Platform. It offers out-of-the-box and customizable dashboards for monitoring application health, advanced log search for log management, and alerting capabilities that notify teams when defined thresholds or anomalies occur.
- **Integration Intelligence** is the next-generation, AI-first observability platform for MuleSoft reimagined and built natively on the Salesforce Platform. This offering uses Data 360 as a unified data layer for the telemetry data; Tableau Semantics as a trusted semantic layer to enable intelligent, actionable insights; Tableau Concierge to achieve AI-assisted troubleshooting; and Tableau Next Dashboards to deliver interactive, visual interfaces that bring together multiple rich data visualizations into a single, cohesive view. Tableau Next also offers customers the ability to build custom dashboards atop the semantic data model shipped with observability features.

This stack also powers the agent-centered tracing that provides customers with full transparency into the non-deterministic end-to-end agentic invocation path, allowing them to observe the agent working at each intermediate step, enabling users to get to the root cause of failures faster and identify any performance bottlenecks.

The Salesforce ecosystem exemplifies the power of the platform. System Integrators (SIs) and consulting partners support customers by developing, configuring, and optimizing intricate Salesforce solutions. Independent Software Vendors (ISVs) build innovative applications and solutions on the platform, which customers can then install into their Salesforce organizations. These ISV apps are available on AppExchange, Salesforce's application store launched in 2006, which now features over 10,000 applications with more than 14.3 million installs as of October 2025.

To help customers navigate the vast marketplace and discover relevant applications, the AppExchange search experience has been re-architected in 2025 to leverage Data 360. Salesforce Data 360’s vector search capabilities work in concert with traditional keyword matching to deliver more semantically relevant results by understanding a user's intent through natural language. The ultimate vision is to evolve this foundation by integrating it with the Agentforce platform, enabling a fully agentic, “ask anything” interface where customers can conversationally describe their business challenges to receive highly personalized solution recommendations.

AppExchange ensures high-quality solutions through a rigorous review process involving code analyzers, security scanners, and reference implementation guides, all in close collaboration with Salesforce. This platform also provides ISVs with license management tools to tailor application licensing and monetization, supporting various pricing models including user-based and consumption-based options.

The "metadata-driven platform" principles enable ISVs to extend Salesforce’s native apps and metadata, easing the development of data models, business logic, and user interfaces. The Salesforce Platform supports a broad range of solutions, from industry-specific applications to highly customized, branded apps that utilize technologies like Lightning Web Components for UI and Apex Code for business logic.

The concept of "packaging" is crucial for the distribution of these apps across various Salesforce orgs. Packaging involves the serialization of metadata into an artifact that can be installed by any Salesforce customer, using underlying technologies designed for metadata management across various environments. A unique aspect of packaging is that it allows installations in environments unknown to the developer.

To enhance control and safety, “manageability” features within packaging enable ISVs to safely upgrade parts of an application because others can’t depend on these parts, while allowing customers to own and manage other parts. For instance, ISVs can set certain metadata, like custom settings, to “managed”, making them invisible and non-editable by the customer, thus preventing disruptions in the customer’s environment. Managed packages include these manageability controls, whereas unmanaged packages treat deployed metadata as customer-created, which can’t be upgraded post-deployment.

Since the inception of the AppExchange and the Salesforce Platform, there's been a notable increase in both the number and complexity of packages being created and installed. In response to these demands, the platform introduced the Second-Generation Packaging Architecture in 2020. This new architecture enhances the modularity of managed packages, improves versioning flexibility, allows for namespace sharing, and supports declarative dependencies, among other advancements in the software development lifecycle. The package deployment architecture also had several significant enhancements for greater efficiencies and scale, such as determining which metadata was changed and only deploying the deltas.

A critical measure for the development of new products and features is their compatibility with packaging and readiness for ISV use. The platform emphasizes the rapid availability of its capabilities to partners, enabling the Salesforce Ecosystem to leverage the innovative potential of the Salesforce Platform effectively and beyond Salesforce’s out-of-the-box offerings. This, however, is an area of ongoing investment to ensure all capabilities described in this document that are available to Salesforce internal developers are also available to our ISV developers.

Additionally, the Heroku Marketplace and Slack Marketplace offer a wide range of third-party integrations and add-ons that can enhance the functionality of Salesforce applications. Heroku Marketplace provides tools and services for additional app functionality, as well as improving how developers build, deploy, and manage applications. Slack Marketplace offers integrations that can streamline workflows and improve collaboration within Salesforce environments.

In the spirit of our core value, Customer Success, Salesforce acts as “Customer Zero” for all applications and services on the Salesforce Platform, leveraging customer-facing products internally wherever possible. This provides significant advantages:

- **Rigorous Product Testing**: By using the product suite daily, Salesforce employees expose the platform to real-world challenges, enhancing product quality and identifying improvement areas.
- **Refined Products**: Immediate feedback from internal use allows for rapid refinement of features and usability, as well as rapid identification and resolution of any bugs, resulting in products that better meet customer needs upon release.
- **Deep Industry Expertise**: Internal use across various functions gives Salesforce valuable insights into specific product and industry challenges, particularly in high-tech sectors.
- **Enhanced Customer Empathy**: Firsthand experience with the platform enables employees to better understand and address customer pain points.
- **Marketing and Sales Insights**: Daily product usage informs sales and marketing strategies, helping to tailor the platform to customer needs.
- **Stronger Go-to-Market Strategy**: Successful internal implementation allows Salesforce to confidently market the suite as a proven solution.

Additionally, all software updates destined for production are initially deployed to a dedicated "Salesforce on Salesforce" Hyperforce instance as part of a staggered deployment process. Since August 2020, this instance has successfully hosted GUS, Salesforce’s org for engineering teams, as well as Salesforce’s CRM operations, showcasing Hyperforce’s robustness and readiness for any customer. This strategy allows internal teams to test and surface any issues well before production deployments to external customers.

The Salesforce Technology organization has fully embraced Agentforce as the internal platform for increased productivity and quality across the SDLC. This has allowed us to not only improve the quality of code we ship to our customers by detecting and mitigating bugs early, but has also enabled us to rapidly iterate on agentic experiences based on first-hand internal feedback.

Since its founding in 1999, Salesforce has experienced multiple technology transformations. However, the transformation involving the Salesforce Platform was particularly significant due to its scale and the rapid pace at which changes were implemented. This transformation required a simultaneous evolution of all major architectural components to achieve an integrated platform. To ensure this transformation was iterative and minimally disruptive to stakeholders and trailblazers, the Salesforce Technology organization also had to evolve its engineering and product delivery practices.

The Salesforce Technology organization is a large and diverse team, comprising over 2500 teams located in more than 20 sites across 14 different countries. This group operates on a grand scale, delivering more than 200 product releases and implementing 250,000 system changes each week. In line with the broader company ethos, the Technology group is guided by five core values: Trust, Customer Success, Innovation, Equality, and Sustainability. These values are integral to shaping the group’s strategy, guiding its execution, and influencing daily decisions.

Adhering to our core values, the Salesforce Engineering 360 framework equips engineering teams with action-oriented dashboards and comprehensive insights into their operations, setting clear expectations for standards and best practices within the organization. This holistic view encompasses various critical areas including availability, security, compliance, quality, accessibility, developer productivity, agile product development, and cost efficiency. To provide these insights, the framework processes billions of records from hundreds of internal engineering systems, such as security systems, production health logs, code repositories, development environments, CI/CD, and release/work planning and tracking systems, all built on the Salesforce Platform utilizing latest innovations from Agentforce, Data 360, Tableau, and Slack.

Rooted in this and other data, the Salesforce Technology organization leverages AI and agentic technologies to accelerate ‌productivity. We have over 10,000 daily active users of internal AI tools and we have built over 100 AI agents that are part of our internal AgentExchange program, driving forward productivity improvements across the organization.

Thanks to our top value of Trust, service ownership is deeply rooted in our engineering culture. Each service and product is designed to not only meet but exceed their Service Level Objectives (SLOs) related to availability and incident management metrics like Time To Detect (TTD) and Time To Restore (TTR). Our approach to change management, release readiness, and problem management adheres to high standards. Security is integrated into every phase of our Secure Development Lifecycle, adhering to the secure-by-default principle. Quality and performance are prioritized through the Agile Testing Methodology, which includes millions of automated tests, across unit, functional, integration, and load/scale tests within our CI/CD pipelines.

Architecturally, we focus on developing shared capabilities to enhance leverage and efficiency, thereby improving quality. For instance, we’ve developed managed services within Hyperforce to meet diverse needs such as compute and data management, enabling product teams to focus on product innovation while central teams enhance these services in terms of security, availability, and cost-efficiency.

Our operations are agile, fostering innovation delivery to customers. Each of the over 3000 teams has the autonomy in how to implement the agile framework, using either Scrum or Kanban. Product development planning across the organization is structured with various timelines, including a 3-year long-range plan for strategic direction, followed by annual execution plans, and further broken down into 4-month product release plans, which inform bi-weekly sprint plans. Products, features, and bug fixes are deployed through multiple release vehicles to cater to diverse customer needs, including three major annual releases, bi-weekly releases, and daily releases.

Productivity is critically important given our scale. We utilize the SPACE framework to measure productivity effectively, supported by a comprehensive set of metrics provided by the Engineering 360 system. We also focus on improving tools and experiences for our internal developers to streamline the development lifecycle, with investments in agentic experiences and AI, workflow, build tools, development setups, safer releases, and security services yielding significant benefits.

In conclusion, the Salesforce Platform has undergone a remarkable transformation over the past five years, evolving from the pioneering multitenant cloud platform to a trusted, integrated, agentic, and data-empowered platform that powers a suite of applications and services in their region of choice. This evolution was driven by the need to address emerging challenges such as the rise of public cloud providers, increasing regulatory demands, and advancements in generative AI and machine learning.

The introduction of Hyperforce, Data 360, and Agentforce has significantly enhanced the platform’s capabilities, ensuring it remains at the forefront of innovation while maintaining trust and reliability. The successful migration of the majority of our customers to this new platform underscores the ingenuity and dedication of our engineers.

As we continue to innovate and adapt to changing market demands, the Salesforce Platform is well-positioned to support the next generation of applications and customer use cases, reaffirming our commitment to customer success and technological excellence.