---
name: Hyperforce
type: concept
category: architecture-pattern
tags: [hyperforce, infrastructure, cloud, security, multitenancy, salesforce]
sources: 2
last_updated: 2026-04-21
---

# Hyperforce

## Definition
Salesforce's current-generation cloud infrastructure platform, deployed on public cloud providers (primarily AWS). Hyperforce replaces Salesforce's first-party data centers and provides the foundational layer for all Salesforce products with built-in compliance, elasticity, and zero-trust security.

## When to Use
Hyperforce is not an optional choice — it's the platform all Salesforce customers run on (95%+ migrated as of 2024). Understanding Hyperforce matters for:
- Data residency and regulatory compliance decisions (EU Operating Zone, GDPR, data sovereignty)
- Security architecture (zero-trust model, encryption key management, CMK/BYOK)
- Availability planning (AZ/region failure scenarios)
- Cost governance (FinOps on public cloud, COIN score)

## How It Works

### Core Architecture Concepts
- **Hyperforce Instance**: Deployment unit mapped to one AWS Availability Region; each instance operates independently; 3+ AZs replicated
- **Hyperforce Cells**: Scale unit within a Functional Domain (≈ traditional "Salesforce instance"); blast radius boundary
- **Supercells**: Logical grouping of Cells for shared services; larger blast radius boundary
- **Functional Domains**: Business functional domains (Sales Cloud, Service Cloud...) + Foundational domains (IAM, logging, monitoring)
- **Operating Zones**: One or more Hyperforce Instances grouped for data residency (e.g., EU Operating Zone; satisfies GDPR data-in-EU requirements)
- **Control Plane**: Redundant Hyperforce Instances in US East; hosts Runtime Manager, Access Management — US East outage makes control plane unavailable even if other regions are running

### Eight Infrastructure Principles
1. **Infrastructure as Code**: Kubernetes/Service Mesh; immutable artifacts; automated on-demand provisioning
2. **Zero-Trust Security**: mTLS between services; just-in-time access; short-lived private keys; least privilege
3. **Managed Services**: Multitenant, multi-cloud services for portability across commercial/government/air-gapped environments
4. **Built-in Resilience**: Mission-critical services across 3+ AZs; cross-instance data replication for backup
5. **Fully Observable**: OpenTelemetry integration; logs, metrics, traces, alerting; OTEL-based distributed tracing
6. **Automated Operations**: AIOps for predictive failure detection and remediation; infrastructure lifecycle automation
7. **Automated Scale**: FinOps-aware autoscaling; abstracts cloud provider account limits
8. **FinOps Aware**: Compute Savings Plans, Spot Capacity, On-Demand Capacity Reservations; COIN score for optimization tracking

### Security Architecture
- **End-to-end encryption**: TLS with PFS cipher suites in transit; hardware security module-backed key management at rest
- **Unique tenant encryption keys**: Each org gets its own encryption key — no cross-tenant key exposure
- **PKI with certificate revocation**: Robust, scalable revocation — addresses common PKI weakness
- **Customized JDK**: FIPS-compliant by default; protects against XXE, XSS, CSRF, SQL injection via SSDL
- **Phishing-resistant MFA**: Hardware-backed keys for production access; CISA Zero Trust principles
- **WAF + IDS/IPS + EDR**: Web application firewall, intrusion detection, endpoint detection and response
- **Incident response**: Predefined procedures specific to Hyperforce failure modes

### Availability Model
- **Within region**: Multi-AZ deployment; automatic replica restart on AZ failure (2-15 min)
- **Cross-region**: No native HA — requires customer-designed architecture (active-active/warm/cold standby)
- **US East dependency**: Control plane in US East — US East outage = control plane unavailable globally
- **Blue/green deployments**: ~1 minute/year maintenance windows

## Key Constraints
- US East region failure impacts Anypoint Platform control plane — Runtime Manager unavailable even for apps elsewhere
- Hyperforce data backup copies to other Hyperforce Instances for BC/DR — not instant replication
- Data residency: each org is in one Hyperforce Instance; cross-instance data movement requires explicit architecture

## Related Patterns / Alternatives
- [[salesforce-platform]] — Hyperforce is the infrastructure layer of the Salesforce Platform
- [[cloudhub-ha-dr]] — CloudHub 2.0 HA/DR patterns for MuleSoft workloads on Hyperforce
- [[data-360-security-architecture]] — ABAC/CEDAR security model that runs on top of Hyperforce

## Dennis's Take
From a customer architecture perspective, Hyperforce matters most for data residency decisions (EU Operating Zone is the key lever for GDPR compliance) and for understanding the US East control plane dependency when planning MuleSoft HA. For most implementations, Hyperforce is invisible — it's the Salesforce-managed foundation you rely on, not architect around.

## Sources
- [[salesforce-platform-transformed-tomorrow]] — Hyperforce Instances/Cells/Supercells, 8 infrastructure principles, security controls, FinOps
- [[platform-multitenant-architecture]] — Platform infrastructure section; Hyperforce as foundation for MT architecture
