---
name: D2C Return to Origin (RTO) — India
type: concept
category: market-term
tags: [d2c, rto, india, cod, bnpl, logistics, fraud]
sources: 1
last_updated: 2026-04-22
---

# D2C Return to Origin (RTO) — India

## Definition
Return to Origin (RTO) is the event where a shipped order is rejected by the customer at delivery and returned to the seller. In Indian D2C, RTO is a major profitability leak — typical RTO rates are 20–40% for Cash on Delivery (COD) orders vs under 5% for prepaid orders. RTO triggers double shipping costs (forward + return), inventory blockage, and packaging loss.

## Why It Matters for Acqura
Primarily relevant if Acqura serves Indian D2C clients. RTO reduces effective order value and distorts paid media economics — high RTO rates mean ROAS from Meta/Google ads is overstated (orders that return are counted as conversions but never generate revenue). This is a data quality problem that feeds upstream into Acqura's measurement layer.

Secondarily relevant: BNPL solutions (Simpl, LazyPay, ZestMoney) are being adopted to reduce COD and RTO — these create structured payment events that generate first-party data for attribution.

## How It Works

### Root Causes
1. **COD dependency**: India's preference for Cash on Delivery — customers can refuse at door; 20–40% RTO for COD
2. **Impulse buying**: COD enables zero-commitment orders; prepaid requires financial intent
3. **Fake/fraudulent orders**: fake addresses, numbers; serial fraudsters gaming return policies
4. **Long delivery times**: reduces excitement; customer unavailability
5. **Price comparison at delivery**: customer finds lower price on Amazon/Flipkart and refuses

### Reduction Strategies
- **BNPL integration**: Simpl, LazyPay, ZestMoney, Amazon Pay Later at checkout → converts COD intent to structured payment commitment
- **Partial COD**: charge small advance (₹50–100) to filter fake orders while preserving COD option
- **OTP verification**: COD orders require OTP before confirmation
- **AI-based RTO prediction**: tools like GoKwik, Razorpay Thirdwatch, Shiprocket X score COD orders for RTO risk before shipping
- **Disable COD for high-risk pin codes**: block COD in historically high-RTO geographies
- **WhatsApp confirmation**: manual confirmation of high-value COD orders via WhatsApp/IVR

## Acqura's Angle
For Indian D2C clients: RTO-adjusted ROAS should be the standard reporting metric, not raw ROAS. If a campaign drives 100 orders with 35% RTO, the effective ROAS is 65% of reported. Acqura's GTI layer should surface RTO-adjusted economics as a default view.

BNPL adoption creates an interesting data opportunity: BNPL providers (Simpl, LazyPay) hold structured payment-intent data that could enrich attribution — potential data partnership angle.

## Contradictions / Open Questions
- How widespread is RTO outside of India — does this problem exist in other COD-heavy markets (Southeast Asia, Middle East)?
- At what BNPL adoption rate does RTO become negligible for a given D2C brand?

## Sources
- [[d2c-rto-reduction-bnpl]] — article covering RTO challenges, BNPL as solution, AI fraud detection tools
