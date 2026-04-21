---
title: Transactional Email Solution Kit
type: source
format: pdf
url: raw/transactional_email_solution_kit.pdf
author: Salesforce
date_published: 2021-01-01
date_ingested: 2026-04-21
tags: [commerce-cloud, marketing-cloud, transactional-email, sftp, solution-kit, winter-22]
---

# Transactional Email Solution Kit

## Summary
Winter '22 solution kit for replacing Commerce Cloud's native email capability with Marketing Cloud Email Studio for transactional emails (order confirmation, shipping notification, order status updates). Pattern: Commerce Cloud exports data to SFTP → Marketing Cloud ingests to data extensions → triggered sends fire on transactional events. B2C Commerce to Marketing Cloud Connector provides hook implementation.

## Key Takeaways

### Architecture Pattern
```
Commerce Cloud (order events)
  → Hook implementation (B2C Commerce → MC Connector)
  → SFTP (catalog, order, customer data feeds)
  → Marketing Cloud Data Extensions
  → Triggered Send (transactional email)
  → Customer
```

### Data Feeds via SFTP
- **Catalog feed**: product catalog data → MC data extension for dynamic content in emails (product images, names, prices)
- **Customer feed**: customer profile data → MC data extension (for personalization, suppression)
- **Order feed**: order data → MC data extension → triggers transactional send on order events
- Feeds are scheduled batch exports (not real-time streaming)

### B2C Commerce → Marketing Cloud Connector
- Provides pre-built hook implementation in Commerce Cloud (SFRA cartridge)
- Hooks fire on order placement, order status changes, shipment events
- Handles SFTP push + MC triggered send invocation
- Reduces custom integration to configuration rather than custom code

### Marketing Cloud Email Studio Advantages Over Native Commerce Email
- Advanced personalization (AMPscript, dynamic content blocks)
- A/B testing and content experimentation
- Deliverability tools (IP warming, reputation monitoring, bounce handling)
- Unified suppression list management across all email programs
- Analytics and engagement tracking (opens, clicks) fed back to CRM via Marketing Cloud Connect

### Performance Considerations
- Design data feed consumption to support expected order volume at peak (e.g., holiday season)
- Data extension indexing: ensure subscriber key + order ID indexed for lookup performance
- Triggered send queue: high-volume scenarios (flash sales) can overwhelm triggered send queue — design with send classification and priority queuing
- Follow Marketing Cloud data extension best practices: normalize where possible, avoid row count explosion

## Notable Quotes / Data Points
- Winter '22 (2021) — SFTP-based approach is established but not real-time; for real-time transactional triggers, Transactional Messaging API is now available in MC
- Native Commerce Cloud email is limited (template customization, analytics) — MC replacement is a common upgrade pattern
- Suppression list management is a compliance benefit: MC manages global opt-outs across all programs

## Wiki Pages Updated
- [[marketing-cloud]] (new entity — to be created)
- [[cross-cloud-data-models]] (new concept — to be created): SFTP as data exchange pattern between Commerce and Marketing

## Gaps / Follow-up
- Read first 150 lines (pdftotext); SFRA cartridge configuration and MC journey builder setup in remainder
- Transactional Messaging API (newer MC capability) would replace SFTP pattern for real-time triggers
- How does Data 360 activation fit here? Real-time data actions could potentially trigger transactional emails without SFTP
