# Foot Locker Australia — AI Prompt Library

---

## Overview

This repository contains a 10-prompt AI library designed to automate high-frequency, repetitive workflows at Foot Locker Australia. The library covers four business functions — Marketing and Promotions, In-Store Operations, Customer Service, and Loyalty and Retention.

Each prompt has been designed using structured prompting principles (role framing, interactive input collection, output constraints, and human-in-the-loop review), tested against real campaign and operational scenarios, and documented with full version histories showing iterative improvement.

**Business field:** Retail — Foot Locker Australia
**Organisation type:** Specialty athletic footwear and apparel retailer, 100+ stores nationally
**Workflow problem:** A lean team spending 20-90 minutes per task on high-frequency, repeatable content that follows the same structure every time

---

## Repository Structure

```
prompt-library/
│
├── workflows/
│   ├── Section-01-Marketing.md
│   ├── Section-02-InStore.md
│   ├── Section-03-CustomerService.md
│   └── Section-04-Loyalty.md
│
└── prompts/
    ├── P01 Promotions/
    │   ├── P01.md
    │   └── P01-Description.md
    ├── P02 Social media/
    │   ├── P02.md
    │   └── P02-Description.md
    ├── P03 Campaign performance/
    │   ├── P03.md
    │   └── P03-Description.md
    ├── P04 Product description/
    │   ├── P04.md
    │   └── P04-Description.md
    ├── P05 Upsell Script/
    │   ├── P05.md
    │   └── P05-Description.md
    ├── P06 Complaint Triage/
    │   ├── P06.md
    │   └── P06-Description.md
    ├── P07 Customer Response/
    │   ├── P07.md
    │   └── P07-Description.md
    ├── P08 Escalation/
    │   ├── P08.md
    │   └── P08-Description.md
    ├── P09 Loyalty Offer/
    │   ├── P09.md
    │   └── P09-Description.md
    └── P10 Win-back/
        ├── P10.md
        └── P10-Description.md
```

Each prompt folder contains two files:
- **P0X.md** — the actual prompt text, ready to paste into any AI tool
- **P0X-Description.md** — documentation covering intended workflow, problem being solved, automation potential, risks and limitations, and full version history with live test evidence

---

## Prompt Library

### Section 01 — Marketing and Promotions

**Trigger:** Campaign event or promotional period confirmed by the Marketing Manager.

| Prompt | Name | Workflow Step | Manual Time | Time with AI |
|---|---|---|---|---|
| P01 | Promotional Email Copywriter | Step 1 of 3 — campaign email drafted and sent to customer database | 45-60 min | ~3 min review |
| P02 | Instagram Caption Copywriter | Step 2 of 3 — 2 caption variants published to Instagram | 20-30 min | ~5 min review |
| P03 | Campaign Performance Summary | Step 3 of 3 — post-campaign report reviewed for ROI | 60-90 min | ~10 min review |

---

### Section 02 — In-Store Experience

**Trigger:** New product arrival confirmed in inventory or scheduled staff briefing event.

| Prompt | Name | Workflow Step | Manual Time | Time with AI |
|---|---|---|---|---|
| P04 | Product Description Writer | Step 1 of 2 — website listing and digital price card copy | 30-45 min | ~6 min review |
| P05 | Staff Upsell Talking Points | Step 2 of 2 — briefing sheet used in daily team huddles | 20-30 min | ~5 min review |

---

### Section 03 — Customer Service and Complaints

**Trigger:** Customer complaint or inquiry received via email, web form, or social media.

| Prompt | Name | Workflow Step | Manual Time | Time with AI |
|---|---|---|---|---|
| P06 | Complaint Triage | Step 1 of 3 — JSON triage record logged to platform | 10-15 min | ~3 min review |
| P07 | Customer Response Draft | Step 2 of 3 — response email reviewed and sent by agent | 15-25 min | ~5 min review |
| P08 | Escalation Summary | Step 3 of 3 — internal brief forwarded to senior management (High urgency only) | 20-30 min | ~5 min review |

---

### Section 04 — Loyalty and Retention

**Trigger:** CRM data trigger (points threshold reached or member inactive 90+ days).

| Prompt | Name | Workflow Step | Manual Time | Time with AI |
|---|---|---|---|---|
| P09 | FLX Loyalty Reward Email | Triggered by points threshold — tier progress email sent to member | 20-30 min | ~5 min review |
| P10 | Win-Back Email | Triggered by 90+ day inactivity — re-engagement email with loss-aversion framing | 20-30 min | ~5 min review |

---

## Design Principles

Every prompt in this library is built on four principles:

1. **Role framing** — each prompt defines who the AI is and what it specifically knows, not just a job title
2. **Structured input collection** — inputs are collected one question at a time with a brief confirmation step before generating
3. **Output constraints** — word counts, format rules, prohibited phrases, and channel-specific requirements are built into every prompt
4. **Human-in-the-loop** — every prompt has a defined review step before the output is used; AI generates, humans approve

---

## Version History Evidence

Each Description file contains a full version history showing the initial prompt, what failed, what was changed, and the lesson learned. Live test outputs are logged for every current version.

The commit history of this repository provides additional evidence of iterative development — earlier commits reflect initial prompt versions, with subsequent commits showing refinements based on testing.

---

## References

- AllAboutAI (2025). *AI in Retail Statistics 2025*. https://www.allaboutai.com/resources/ai-statistics/ai-in-retail/
- HubSpot (2025). *2025 Global Social Media Trends Report*. https://blog.hubspot.com/sales/average-email-open-rate-benchmark
- MailerLite (2025). *Email Marketing Benchmarks 2025*. https://www.mailerlite.com/blog/compare-your-email-performance-metrics-industry-benchmarks
- Morgan Stanley (2024). *Retail Technology Trends: AI & Automation Lead Industry Growth*. https://www.morganstanley.com/ideas/retail-technology-trends-2024
- Opensend (2025). *Email Click-Through Rate Statistics for eCommerce Stores*. https://www.opensend.com/post/email-click-through-rate-ecommerce
- PwC (2024). *AI-Powered Retail Reinvention: Why Now Is the Time*. https://www.pwc.com/gx/en/services/alliances/microsoft/ai-retail-transformation-future.html
- Salesforce (2024). *State of the Connected Customer*. https://www.salesforce.com/resources/research-reports/state-of-the-connected-customer/
- Shopify (2025). *AI in Retail: Use Cases and Implementation Guide*. https://www.shopify.com/enterprise/blog/ai-in-retail