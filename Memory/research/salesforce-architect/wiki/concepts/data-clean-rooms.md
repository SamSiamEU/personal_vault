---
name: Data Clean Rooms
type: concept
category: data-pattern
tags: [clean-rooms, privacy, zero-copy, data-360, collaboration, pets]
sources: 1
last_updated: 2026-04-21
---

# Data Clean Rooms

## Definition
A secure, governed environment enabling multiple parties to generate joint analytics and AI insights without exposing or exchanging raw data. Modern clean rooms use a federated, zero-copy model where computation occurs at the data source and only privacy-compliant aggregated results are shared.

## When to Use
- Cross-organizational data collaboration where raw data cannot be shared (regulation, competition, privacy)
- AdTech: campaign attribution, reach/frequency measurement, audience overlap without cookies
- Retail: CPG brands + retailer point-of-sale data collaboration for closed-loop attribution
- Financial services: multi-bank fraud detection without sharing customer records
- Healthcare: cross-provider patient cohort analysis under HIPAA
- Any scenario requiring "compute on shared signal, share only aggregated outcome"

## How It Works

### Clean Room Architecture Evolution

**Traditional ("Bunker") Model:**
- All parties copy data into a neutral third-party environment
- Centralized aggregation; custody partially relinquished
- High latency, high cost, complex legal agreements

**Modern (Federated/Zero-Copy) Model:**
- Data stays in each owner's environment
- Governance layer intercepts queries, enforces privacy at execution time
- Only approved, aggregated results returned
- Lower latency, reduced cost, better regulatory alignment

### Salesforce Data 360 Clean Room Architecture

**Infrastructure**: Runs on Hyperforce (AWS region); supports cross-cloud collaboration with AWS Clean Rooms.

**Data Pipeline** (before clean room queries):
1. Connect → Persist (Parquet/Iceberg) → Harmonize (DMOs) → Unify (Identity Resolution/Golden Record) → Derive Insights → Act

**Privacy-Enhancing Technologies (PETs)** — mandatory, platform-enforced:
| Technology | Mechanism | Guarantee |
|-----------|-----------|-----------|
| **Differential Privacy** | Calibrated noise injection; tracks privacy budget per dataset | Mathematical proof — presence/absence of individual doesn't affect output |
| **Secure Identifier Alignment** | Deterministic hashing/tokenization; comparisons occur without revealing raw IDs | Enables "join-like" behavior without data disclosure |
| **Aggregation Thresholds** | Minimum record count (e.g., 100) per output | Prevents small-segment re-identification attacks |
| **Result Suppression** | Blocks outputs below minimum threshold | Enforced at platform level — non-overridable |

**Audit DMO**: Immutable audit trail capturing every query execution, policy applied, timestamp, and requester identity.

**Data Spaces**: Logical isolation within org — only objects in the scoped data space are visible to clean room collaborators.

**Einstein Trust Layer integration**: Acts as "architectural airlock" for AI agents — LLM calls on clean room data have zero-data-retention; PII masking applied.

### Use Case Templates
Salesforce provides out-of-the-box templates for:
- Audience overlap analysis
- Segment suppression
- Reach and lift measurement
- Lookalike modeling (AI-powered)

Custom templates allow domain-specific or partner-specific analytical logic without raw data exposure.

### Deployment Workflow
1. **Define objective** — what question, what activation path, what regulatory constraints
2. **Prepare data** — ingest, harmonize, identity resolution (quality here directly impacts match rates)
3. **Provision clean room** — license validation, data space scoping, define governance rules (aggregation thresholds, join keys, allowed SQL operations)
4. **Connect parties** — OAuth-based access with principle of least privilege; Salesforce-to-Salesforce or multi-cloud
5. **Monitor** — query execution, audit DMO, Digital Wallet consumption alerts

### Connectivity Models
- **Salesforce-to-Salesforce**: Via Data Cloud One or approved cross-org sharing; instant setup via shared metadata
- **External cross-cloud (AWS/Snowflake)**: Zero-copy federation; data stays in resident cloud; compute pushed to source

## Key Constraints
- Zero-copy doesn't eliminate compute costs — execution still happens at source; query patterns must be optimized
- Identity resolution quality is the critical upstream dependency — poor match rates = low clean room value
- Privacy budget (differential privacy) is finite per dataset — high-frequency queries exhaust it; must be managed
- Cross-cloud clean rooms require region alignment for data residency compliance

## Related Patterns / Alternatives
- [[data-360-architecture]] — The upstream data platform providing harmonized DMOs for clean room input
- [[data-360-security-architecture]] — ABAC/CEDAR, data spaces, and consent propagation that govern clean room access

## Dennis's Take
Clean rooms are becoming standard infrastructure in regulated industries and any brand that collaborates with retailers or publishers. The Salesforce implementation's biggest differentiator is native activation — insights flow directly to Marketing Cloud without raw data ever leaving the governed boundary. This closes the "insight-to-action gap" that most standalone clean room vendors leave open.

## Sources
- [[data-360-clean-rooms]] — Full clean room architecture, PETs, use cases across industries, deployment workflow
