# Data Model

## Overview

The project uses a lightweight relational structure built in Google Sheets to simulate CRM and Revenue Operations datasets.

The model separates:
- lead-level data
- opportunity lifecycle data
- historical activity logs

This structure supports:
- funnel reporting
- lifecycle tracking
- KPI analysis
- operational auditing

---

# Entity Relationship Overview

```text
leads
   │
   └── lead_id
          │
          ▼
opportunities
          │
          ▼
activity_log
```

---

# Table: leads

Stores inbound lead information and qualification attributes.

## Primary Key
`lead_id`

## Columns

| Column | Description |
|---|---|
| lead_id | Unique lead identifier |
| created_at | Form submission timestamp |
| name | Lead name |
| email | Cleaned email address |
| company | Company name |
| country | Normalized country |
| source | Acquisition source |
| score | Numerical lead score |
| score_band | Low / Medium / High |
| status | Lead lifecycle status |
| region | API-enriched region |
| subregion | API-enriched subregion |

---

# Table: opportunities

Stores pipeline stage progression events.

## Primary Key
`opp_id`

## Foreign Key
`lead_id → leads.lead_id`

## Columns

| Column | Description |
|---|---|
| opp_id | Unique opportunity identifier |
| lead_id | Associated lead |
| stage | Pipeline stage |
| value_estimate | Estimated deal value |
| created_at | Opportunity creation timestamp |
| updated_at | Latest stage update timestamp |

---

# Table: activity_log

Stores historical operational actions and lifecycle events.

## Columns

| Column | Description |
|---|---|
| timestamp | Event timestamp |
| lead_id | Associated lead |
| action | Activity type |
| notes | Additional event details |

---

# Design Decisions

## Separate Leads and Opportunities

This mirrors CRM-style architecture where:
- leads represent people/accounts
- opportunities represent sales pipeline events

This separation enables:
- funnel analysis
- conversion tracking
- revenue reporting

---

## Activity Logging

Maintaining a historical log allows:
- operational traceability
- lifecycle auditing
- stage movement analysis

---

# Relational Logic

## One-to-Many Relationship

One lead may generate multiple opportunity stage events over time.

Example:
- Lead Created
- Demo Booked
- Proposal Sent
- Closed Won

This structure supports chronological funnel tracking.

---

# Analytical Benefits

The data model enables:
- conversion rate analysis
- pipeline stage reporting
- acquisition channel analysis
- geographic segmentation
- revenue forecasting
