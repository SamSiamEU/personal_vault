---
name: Analytics Maturity Model (Kaushik)
type: concept
category: framework
tags: [analytics, maturity, measurement, iabi, segmentation, 10-90-rule, kaushik]
sources: 1
last_updated: 2026-04-24
---

# Analytics Maturity Model (Kaushik)

## Definition

A three-phase model describing how organisations develop analytics capability over time, from basic data capture to business impact. Developed by Avinash Kaushik. Defines the core elements of a functioning analytics practice, the inputs required to make it useful, and the outputs it should eventually produce. Practically useful for diagnosing where an Acqura client sits and what they need before GTI recommendations are meaningful.

## Why It Matters for Acqura

Most Acqura clients arrive in Phase 1 or early Phase 2 — they have basic tracking, run some reports, and make gut-feel decisions. A small number are in Phase 2–3. Almost none are at IABI (Insights → Actions → Business Impact), which is exactly where Acqura's GTI output is positioned.

Understanding the maturity phase helps Acqura calibrate what it offers:
- **Phase 1 client**: GTI needs to start with tracking health, not intelligence
- **Phase 2 client**: GTI supplements their reporting with insight and recommendations
- **Phase 3 client**: GTI can operate as the intelligence layer they lack time/capacity to build internally

The 10/90 rule is also directly relevant to Acqura's positioning: the market has over-invested in tools (GA4, attribution platforms) and under-invested in intelligence (the 90). Acqura sells the 90.

## The Five Core Analytics Elements

Built progressively — each layer enables the next:

1. **Metrics** — a number. Sessions, revenue, clicks. The raw material.
2. **KPIs** — metrics tied to specific business objectives. Can't define a KPI without knowing the objective. Bounce rate will never be a KPI (improving it doesn't change the business).
3. **Dimensions** — attributes of visitors/people. Traffic source, device, geography, campaign. Appear as rows; metrics appear as columns.
4. **Custom Reports** — forcing function for analytical thinking. Standard reports are data pukes. Custom reports require knowing what question you're answering.
5. **Advanced Segmentation** — the separator. "All data in aggregate is crap." Slicing by acquisition, behaviour, and outcomes reveals what's actually happening. The most important skill in analytics.

## Inputs to the Analytics System

**Left-side inputs** (strategic context):
- Business priorities — from the highest leader who'll engage; without this, analysis goes into the shredder
- Competitive reality — who competitors are, where they get traffic, what they do differently
- New opportunities — market shifts that require updated analytical framing

**Top and bottom inputs**:
- Analysts / Big Brains (top) — the 90 in the 10/90 rule; more important than any tool
- Tools (bottom) — the 10; enables, does not generate insight

**The 10/90 rule**: $10 on tools and implementation, $90 on analysts and big brains. Inverting this ratio is the most common analytics failure mode.

## The Three Output Stages

Organisations move through outputs as their analytics practice matures:

1. **Data Pukes** — raw reports, auto-scheduled, sent to everyone. A natural phase; not a failure. Red flag: leadership only asks for *more* reports, never asks questions.
2. **Custom Data Pukes (CDPs)** — targeted reports built to answer specific team needs. Paid Search gets their view; Content gets theirs. Better, but still data — not insight.
3. **IABI — Insights, Actions, Business Impact** — the goal state:
   - **I (Insight)**: "Data suggests X happened. The causal reasons are Y and Z." Most analysts stop at X. The best find Y and Z.
   - **A (Action)**: Specific recommendation — "Triple investment in these keywords." Not a chart. A decision.
   - **BI (Business Impact)**: Quantified — "This will increase revenue by $893k/week." Requires forecasting capability and Finance collaboration.

IABI is what Acqura's GTI should deliver. Most analytics organisations never reach it.

## Three Execution Phases

**Phase 1 — Data Capture (0–6 months)**
Tool implementation, baseline metrics, KPI identification, data quality control. Foundation. Don't try to implement everything at once.

**Phase 2 — Data Reporting (6–12 months)**
Data pukes → custom data pukes. Leadership starts valuing data. Investment in analysts/Big Brains unlocked. Segmentation skills begin to develop.

**Phase 3 — Data Analysis (12+ months, never ends)**
Insight identification → competitive intelligence → business impact computation. Phase 3 organisations identify new business opportunities from data. Two years to get here; the phase never ends — you just get better.

## Acqura's Angle

Acqura's GTI lives at Phase 3 output level. The challenge: many clients are in Phase 1 or 2, which means:
- Their data is not clean enough for reliable GTI inputs (tracking gaps, missing dimensions, no segmentation)
- They don't have internal Big Brains to act on IABI-level outputs — they need the recommendation pre-packaged
- The concept of "action" and "business impact" may be unfamiliar if they've only ever received data reports

This creates an onboarding design problem: Acqura should assess maturity phase at intake and adjust its output format accordingly. A Phase 1 client gets a tracking health audit first. A Phase 2 client gets custom insight reports as a bridge. Only a Phase 3 client gets full GTI/IABI output from day one.

The 10/90 rule is Acqura's market positioning argument in disguise: the market has spent the last decade building better tools (GA4, CAPI, attribution platforms) and almost nothing on the intelligence layer above them. Acqura sells the 90.

## Contradictions / Open Questions

- How does the 10/90 rule apply in 2026 when AI can automate a significant portion of Phase 2 and 3 work? Does the ratio shift, or does it just change *what* the Big Brains should be doing?
- IABI assumes a human can act on the recommendation. If the action is "reallocate budget," does that happen inside Acqura's platform, or does it require the client to act in each ad platform?
- Phase 3 assumes competitive intelligence is available and structured — for SMB clients, this data is thin or expensive. Does Acqura have a role in competitive intelligence gathering?

## Sources

- [[kaushik-digital-analytics-ecosystem]] — primary source; all framework elements, IABI definition, 10/90 rule, three-phase maturity model
