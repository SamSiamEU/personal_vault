We've been offering support for the Meta Conversions API in Weld for some time now, and with the privacy landscape continuing to evolve in 2026, it's more important than ever. Here's a comprehensive, step-by-step guide to help you get the most out of it. Let's dive in.

## Introduction

Traditionally, the client-side Meta Pixel (formerly known as the Facebook Pixel) has been the primary tool for sending conversion signals to Meta. By embedding the pixel on their websites, advertisers have tracked and relayed customer activity to Meta's ad systems. This data powers (1) retargeting audiences, (2) Meta's machine learning models for attribution and targeting, and (3) campaign optimization via Advantage+ and other automated tools.

However, pixel-based tracking has become increasingly unreliable. Third-party cookies have been deprecated across all major browsers. Chrome completed its phaseout in 2025, joining Safari and Firefox. Ad-blocker usage continues to grow, now affecting over 40% of web users globally. Combined with privacy regulations like GDPR, ePrivacy, and the Digital Markets Act (DMA), client-side-only tracking now captures as little as 50-60% of actual conversion events.

The [Conversions API from Meta](https://weld.app/connectors/facebook-conversions) (also known as Facebook Conversion API or "CAPI") solves this by sending events directly from your servers to Meta, bypassing the user's browser entirely. This server-side approach lets you securely transmit conversion signals and first-party customer data to fill the gap left by lost client-side events.

We've observed that companies relying only on client-side tracking see just 50-65% of conversions inside Meta Ads Manager. After implementing CAPI, that number jumps to 95%+, resulting in significantly better campaign targeting, more accurate attribution, and lower cost per conversion.

![Weld Facebook Conversion API - server-side and client-side tracking flow](https://weld.app/_next/image?url=%2Fblog%2Fboost-facebook-conversion-tracking-to-95-with-server-side-tracking-a-step-by-step-guide%2Fweld-facebook-conversion-api.png&w=3840&q=75)

*In addition to the client-side Meta Pixel, it is now essential to also send events server-side with CAPI to avoid event loss and maintain data accuracy.*

## Why CAPI is essential in 2026

The Conversions API is no longer optional. Meta now considers it a baseline requirement for serious advertisers. Here's why:

- **Third-party cookies are gone.** Chrome's 2025 deprecation was the final domino. Server-side tracking is now the primary reliable signal source.
- **Event Match Quality (EMQ) directly affects ad performance.** Meta uses your EMQ score (rated 1-10 in Meta Events Manager, formerly Facebook Events Manager) to determine how well your server events match to Meta accounts. Higher EMQ = better optimization and lower CPAs.
- **Datasets are now the architecture layer.** Meta's modern setup centers on [datasets](https://www.facebook.com/business/help/5270377362999582), which unify website, app, offline/store, and messaging event data into a single pipeline. This means CAPI is no longer just a web-tracking hardening tactic — it is Meta's central event-ingestion layer for all conversion signals.
- **Advantage+ and AI-powered campaigns depend on signal quality.** Meta's automated campaign tools rely heavily on complete conversion data. Incomplete data leads to poor optimization and wasted budget.
- **The legacy Offline Conversions API was discontinued in May 2025.** If you were previously using Meta's Offline Conversions API to upload store sales or other offline events, you must now use the Conversions API instead. CAPI handles offline events natively when you set `action_source` to `physical_store`.

## Implementing Meta CAPI can be challenging

While CAPI is a powerful tool, it can pose significant implementation challenges due to the technical proficiency required to extract data from your sources and send it to the API.

On the B2C side, if you're a single-channel brand (e.g. a Shopify store), you have tools like [Data Sharing](https://help.shopify.com/en/manual/promoting-marketing/analyze-marketing/meta-data-sharing) from Shopify that make it easy. WooCommerce has a [similar solution](https://woocommerce.com/posts/adapt-for-the-future-with-facebook-conversions-api/).

But what if you're an omni-channel B2C or B2B brand, with data spread across your website, retail POS, Amazon, CRM, and more? There is no "one-click" solution for that.

This is where [Weld](https://weld.app/) comes in. As an ELT and Reverse-ETL platform, Weld automates the synchronization of conversion events with our direct integration with Meta CAPI, eliminating the need for custom [API development](https://developers.facebook.com/docs/marketing-api/conversions-api/using-the-api) and ongoing maintenance.

Meta also offers native tooling like the [Conversions API Gateway](https://developers.facebook.com/docs/marketing-api/conversions-api/guides/gateway) for managed single-source deployments, and the [Parameter Builder Library](https://developers.facebook.com/docs/marketing-api/conversions-api/parameter-builder-library) for generating match keys. However, these tools are designed for simpler setups. When you need to orchestrate data from multiple sources like CRM, POS, databases, and e-commerce platforms into a unified event stream, Weld is the stronger choice.

## Sending events both client-side and server-side (redundant setup)

Meta strongly recommends a **redundant setup**: sending the same events via both the Meta Pixel (client-side) and the Conversions API (server-side). This ensures maximum event coverage.

Keep your current Pixel implementation and treat CAPI as an addition to boost accuracy. You'll send some events twice, but Meta handles deduplication automatically when you include the proper identifiers.

Meta supports two deduplication methods:

1. **Event ID + Event Name (recommended):** Include matching `event_id` and `event_name` on both client and server events. The Meta Pixel's `eventID` must match the Conversions API's `event_id`. Events with the same combination received within 48 hours are deduplicated.
2. **FBP / External ID (fallback):** If generating a shared `event_id` across your client and server is difficult, you can instead pass `fbp` and/or `external_id` consistently on both channels. Meta will use these to deduplicate. This is especially useful when your browser and server systems don't share a common transaction ID. Note: this method only deduplicates browser events that arrive *before* the server event.

We recommend method 1 as the default, with method 2 as a safety net. For the highest reliability, **send all three identifiers** (`event_id`, `external_id`, and `fbp`) whenever possible. We'll show you how to implement this in the guide below.

## Use-Cases for Meta CAPI with Weld

### Use-case 1: Omni-channel retailer (online + physical stores)

You're a retailer using Meta Ads to drive traffic to your online store and physical locations. You have the Meta Pixel tracking **PageView**, **AddToCart**, and **Purchase** events on your website.

With ad-blockers and cookie restrictions, you're only seeing about 55% of online conversions in Meta. And Meta has zero visibility into purchases made at your physical stores, which could be nearly half your transactions.

With CAPI via Weld, you can send both the missing online events and your in-store purchases (using `action_source: physical_store`) to Meta, giving the ad platform a complete picture for optimization. For offline/physical store events, `event_time` can go up to 62 days back, compared to 7 days for web events.

> **Note:** If you were previously sending store data via Meta's legacy Offline Conversions API, you should migrate to the Conversions API. The old API was discontinued in May 2025, and CAPI is now the only supported path for offline events.

### Use-case 2: B2B SaaS with lead funnel events

You're a B2B company running Meta lead-gen campaigns. Your funnel has multiple stages (form submission, demo booked, qualified lead, closed deal), but the Pixel only sees the initial form fill.

With CAPI, you can send downstream funnel events (e.g. `Lead`, `CompleteRegistration`, or custom events) from your CRM directly to Meta, using the [Conversion Leads Integration](https://developers.facebook.com/docs/marketing-api/conversions-api/conversion-leads-integration). This trains Meta's algorithm to optimize for leads that actually convert, not just those that fill out a form.

### Use-case 3: App + web business

You have both a website and a mobile app. The Conversions API now supports [app events](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) through the same unified endpoint, so you can send app install, purchase, and engagement events alongside your web events, all through a single Weld Reverse-ETL sync.

Below, we'll walk through how to set this up in Weld.

## Step 1: Create a Weld account

Weld is your gateway to simplified data engineering, offering automated data pipelines from 300+ data sources (SaaS, databases, files etc.) and an AI-driven SQL Editor to build trustworthy data models.

Push data models to dashboards in your BI Tool (PowerBI, Tableau, Metabase, Looker etc.) or use our Reverse-ETL feature to send data directly to CRM, ad platforms, and more. Today, we'll use Reverse-ETL to push events to Meta CAPI.

All of this runs on your own data warehouse. Weld supports Google BigQuery, Snowflake, and more.

Sign up for a free account at [weld.app](https://weld.app/). It only takes a few minutes, and you'll get access to the Meta CAPI integration.

## Step 2: Connect your data sources

Get your server-side data into Weld with our pre-built integrations. Set up data sources in minutes in the Weld app, where you'll be guided through the flow.

Systems where you typically find relevant customer data: CRM (HubSpot, Salesforce), e-commerce platforms (Shopify, WooCommerce), POS systems, databases, Google Sheets, CSV files, etc.

![Connect data sources in Weld](https://weld.app/_next/image?url=%2Fblog%2Fboost-facebook-conversion-tracking-to-95-with-server-side-tracking-a-step-by-step-guide%2Fdata_sources_example.png&w=2048&q=75)

*You can connect to 300+ tools with one click in Weld.*

If you're unsure about how to set up your first data pipeline, check out our [Product Tour](https://weld.app/product-tour-video).

## Step 3: Build your data model for conversion events

With your data sources connected, build a SQL data model in Weld that shapes the data you'll send to Meta CAPI. For detailed field-mapping guidance, see our [Facebook Conversions API docs](https://weld.app/docs/applications/facebook-conversions-api).

To maximize your **Event Match Quality (EMQ)** score, include as many of the following [parameters](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/) as possible:

**Required parameters:**

- **event\_name** — the conversion event (e.g. Purchase, Lead, AddToCart)
- **event\_time** — UNIX timestamp of when the event occurred
- **action\_source** — where the event happened (e.g. `website`, `physical_store`, `app`)

**Recommended for high EMQ (customer information):**

- **email** (em) — hashed by Weld automatically
- **phone** (ph) — hashed by Weld automatically
- **first\_name** (fn) + **last\_name** (ln) — hashed by Weld automatically
- **client\_ip\_address** — do NOT hash
- **client\_user\_agent** — do NOT hash (required for web events)
- **fbc** (click ID) — the `_fbc` cookie value, do NOT hash
- **fbp** (browser ID) — the `_fbp` cookie value, do NOT hash
- **external\_id** — your internal user/customer ID, hashing recommended
- **event\_source\_url** — the URL where the event occurred (required for web events)

**For deduplication:**

- **event\_id** — must match the `eventID` you pass with the Meta Pixel

**For offline/physical store events:**

- **city** (ct) — lowercase, hashed
- **country** — 2-letter ISO code, hashed
- **state** (st) — 2-letter code, hashed
- **zip** (zp) — hashed

Weld handles all required hashing automatically for customer information parameters. Always ensure you have user consent before collecting and sending this data.

> **Tip: Refresh `fbp` and `fbc` regularly.** These are cookie values that change over time. If you capture and store them, make sure you're sending the most recent values. Stale cookies reduce match quality.

**Tips for the event\_id:** You need the same `event_id` on both the client-side Pixel and server-side CAPI for deduplication to work. A common pattern is to combine the event name with a unique identifier:

```sql
{event_name}:{order_id}
```

or for SaaS:

```sql
{event_name}:{user_id}:{timestamp}
```

The way Meta handles this is described in their [deduplication docs](https://developers.facebook.com/docs/marketing-api/conversions-api/deduplicate-pixel-and-server-events/):

> If we find the same server key combination (**event\_id** and **event\_name**) and browser key combination (**eventID** and **event**) sent to the same Pixel ID within 48 hours, we discard the subsequent events.

On the client side, pass the event\_id like this:

```js
fbq(
  "track",
  "Purchase",
  { value: 12, currency: "USD" },
  { eventID: "Purchase:order_123" },
);
```

![SQL data model for Meta CAPI in Weld](https://weld.app/_next/image?url=%2Fblog%2Fboost-facebook-conversion-tracking-to-95-with-server-side-tracking-a-step-by-step-guide%2Freverse_etl_example.png&w=2048&q=75)

*An example SQL data model to fetch data for Meta CAPI*

## Step 4: Send data to Meta CAPI with Weld Reverse-ETL

Set up the Reverse-ETL sync directly from the SQL editor with your data model. Follow the steps in Weld where you'll map your model columns to the Meta CAPI parameters. This takes just a few minutes. For the full walkthrough, see our [setup guide](https://weld.app/docs/applications/facebook-conversions-api).

![Export to Meta CAPI with Weld Reverse-ETL](https://weld.app/_next/image?url=%2Fblog%2Fboost-facebook-conversion-tracking-to-95-with-server-side-tracking-a-step-by-step-guide%2Freverse_etl_example_mapping.png&w=2048&q=75)

*Send data to Meta CAPI with Weld Reverse-ETL in a few clicks*

Select a sync schedule (e.g. every 30 minutes) and Weld will automatically push new events to Meta. Meta recommends sharing events as close to real time as possible for best optimization results.

Start the sync and see data flow immediately. Any errors will be displayed in Weld and we'll notify you via email. Common errors include formatting issues. For example, "city" must be lowercase and "country" must use 2-letter ISO codes. See the full [formatting requirements](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters).

## Step 5: Test before going live

Before running your sync in production, validate your integration:

1. **Build your payload with [Payload Helper](https://developers.facebook.com/docs/marketing-api/conversions-api/payload-helper)** — Meta's tool generates the correct payload structure for your events and recommends which parameters to include.
2. **Send test events with `test_event_code`** — In Meta Events Manager, go to the Test Events tab to get your test event code. When you add this code to your CAPI payload, Meta routes events to the testing view instead of production, so you can validate without affecting live data.
3. **Verify in Meta Events Manager** — Confirm your test events appear with the correct parameters, event names, and deduplication status.
4. **Check Event Match Quality (EMQ)** — Review the EMQ score for each event type. Aim for **6+ out of 10**. If it's low, add more customer information parameters to your SQL model.
5. **Remove the test code** — Once validated, remove the `test_event_code` from your payload and start your production sync.

## Step 6: Monitor ongoing integration health

Setup is not a one-time task. Your CAPI integration needs ongoing monitoring to maintain performance:

- **Event Match Quality (EMQ):** Check weekly in Meta Events Manager. If EMQ drops, investigate whether customer data coverage has changed (e.g. fewer emails being captured).
- **Deduplication rate:** Monitor what percentage of events are being deduplicated vs. double-counted. A healthy redundant setup should show clear dedup activity.
- **Data freshness:** Meta performs better when events arrive close to real time. If your sync schedule drifts or your upstream models lag, freshness drops and optimization suffers.
- **[Dataset Quality API](https://developers.facebook.com/docs/marketing-api/conversions-api/dataset-quality-api):** For teams managing CAPI at scale, Meta offers a programmatic API to monitor event quality, match rates, and diagnostics, which is useful for building automated alerts if key metrics drop.
- **Review dataset diagnostics weekly:** Check Meta Events Manager for warnings about invalid parameters, low match rates, or rejected events.

Set up alerts in your data stack to flag issues early. For example, if the number of events sent drops significantly or EMQ falls below a threshold.

## Proving the lift: How to show CAPI is working

After implementing CAPI, you'll want to prove the business impact, not just confirm events are flowing. Here's how:

### Track "Additional conversions reported"

Meta surfaces an "Additional conversions reported" metric in Meta Events Manager that shows how many extra conversions were captured thanks to your server-side integration vs. Pixel alone. This is the most direct proof that CAPI is creating measurement lift. If you don't see this metric, check that you have both Pixel and CAPI sending the same events, since the comparison requires both channels to be active.

### Compare pre/post metrics

Track these KPIs before and after your CAPI launch:

- **Total conversions reported** — should increase by 20-40% depending on how much data was previously lost.
- **Event Match Quality (EMQ) score** — should trend upward as you add more customer parameters.
- **Cost per conversion** — should decrease as Meta's algorithm receives better signal quality.
- **Deduplication rate** — a healthy redundant setup (Pixel + CAPI) should show consistent dedup activity, confirming events are being merged correctly rather than double-counted.

### Run a Conversion Lift Study

For rigorous measurement, Meta offers [Conversion Lift Studies](https://developers.facebook.com/docs/marketing-api/guides/lift-studies) that quantify the incremental impact of your server events on campaign performance. This is especially valuable for larger advertisers who need to justify the investment to stakeholders.

### Connect to your paid-media reporting

Tie your CAPI performance data back to your BI dashboards. With Weld, your conversion event data is already in your data warehouse, so you can compare Meta Ads Manager reporting with your internal source-of-truth data, spot discrepancies, and quantify the accuracy improvement.

---

## Conclusion

In 2026, the Meta Conversions API is no longer a nice-to-have. It's essential infrastructure for any advertiser running Meta campaigns. With third-party cookies gone, the legacy Offline Conversions API discontinued, and Meta's AI-driven campaign tools demanding high-quality conversion signals, server-side tracking is the foundation of effective paid media.

The challenge has always been implementation, especially for omni-channel brands with data scattered across web, retail, CRM, and app platforms. Weld eliminates that complexity by letting you build a SQL model over your warehouse data and sync it directly to Meta CAPI, with no custom API code to build or maintain.

Here's what we covered in this guide:

- **Why CAPI matters in 2026:** Cookie deprecation, datasets as the architecture layer, the Offline Conversions API sunset, Event Match Quality, and Meta's unified CAPI endpoint.
- **Use-cases:** Omni-channel retail (including offline/store events), B2B lead funnels, and app+web businesses.
- **Step-by-step setup:** Connecting data, building your SQL model, mapping parameters, configuring deduplication, testing with `test_event_code`, and monitoring ongoing health.
- **Proving the lift:** Tracking additional conversions reported, comparing pre/post metrics, and running Conversion Lift Studies.

By implementing CAPI with Weld, you can expect 95%+ event accuracy, better campaign optimization through higher EMQ scores, and ultimately lower cost per conversion.

Ready to get started? [Sign up for Weld](https://weld.app/) and check out our [Facebook Conversions API documentation](https://weld.app/docs/applications/facebook-conversions-api) for the full setup walkthrough.

## Sources

- [Meta Conversions API Documentation →](https://developers.facebook.com/docs/marketing-api/conversions-api/)
- [CAPI Parameters Reference →](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/)
- [Customer Information Parameters (formatting rules) →](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters)
- [Deduplication Guide →](https://developers.facebook.com/docs/marketing-api/conversions-api/deduplicate-pixel-and-server-events/)
- [Best Practices →](https://developers.facebook.com/docs/marketing-api/conversions-api/best-practices)
- [CAPI for Offline Events →](https://developers.facebook.com/docs/marketing-api/conversions-api/offline-events)
- [Dataset Quality API →](https://developers.facebook.com/docs/marketing-api/conversions-api/dataset-quality-api)
- [Parameter Builder Library →](https://developers.facebook.com/docs/marketing-api/conversions-api/parameter-builder-library)
- [Conversion Leads Integration (B2B) →](https://developers.facebook.com/docs/marketing-api/conversions-api/conversion-leads-integration)
- [Weld Facebook Conversions API Docs →](https://weld.app/docs/applications/facebook-conversions-api)