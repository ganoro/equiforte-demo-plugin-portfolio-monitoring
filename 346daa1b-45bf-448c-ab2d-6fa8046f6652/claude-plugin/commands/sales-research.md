---
name: sales-research
description: Start a structured research loop on financial companies
tags:
  - research
  - analysis
  - deep-dive
  - pe
  - vc
placeholder: "e.g. Research Private Equity companies in Toronto"
defaultOutput: Document
icon: IconSearch
arguments:
  - name: topic
    description: The research topic, question, or analysis request
    required: true
---

# /sales-research — Start a structured research loop on financial companies

## Purpose

This skill performs **targeted research on financial firms** (private equity, hedge funds, private credit, venture capital, asset managers) to support **selling an AI platform**.

The goal is to produce **actionable go-to-market intelligence**, including:

* Identifying **decision makers (ICP)** such as CFO, CTO, Head of AI/Data
* Understanding **firm structure and operational pain points**
* Mapping **LP relationships**
* Discovering **events, conferences, and channels** where decision makers are active
* Identifying **AI opportunities** (LP reporting, audit readiness, operations automation)

The output is a **personalized outreach strategy** including potential **email angles, event targeting, and messaging**.

---

# Inputs

| Input               | Description                                                                    | Required |
| ------------------- | ------------------------------------------------------------------------------ | -------- |
| `firm_name`         | Name of the target financial firm                                              | Yes      |
| `firm_type`         | Private equity / hedge fund / private credit / venture capital / asset manager | No       |
| `region`            | Geographic focus                                                               | No       |
| `research_depth`    | quick / standard / deep                                                        | No       |
| `ai_use_case_focus` | LP reporting / portfolio monitoring / deal sourcing / compliance / operations  | No       |

Example:

```
firm_name: KKR
firm_type: private equity
research_depth: deep
ai_use_case_focus: LP reporting, operational automation
```

---

# Core Objective

Identify **how an AI platform can solve real operational pain points** inside the firm.

Focus on:

* **Investor reporting**
* **portfolio data consolidation**
* **fund reporting**
* **audit documentation**
* **compliance**
* **internal analytics**

Private equity firms often rely on **fragmented data systems and manual processes**, particularly for investor reporting and portfolio monitoring. ([Acquis Consulting][1])

LP reporting alone can require **hundreds of hours per quarter** due to manual data reconciliation and normalization across portfolio companies. ([Acquis Consulting][1])

LPs increasingly expect **on-demand access to fund data and better transparency**, which pressures GPs to modernize reporting infrastructure. ([henon.ai][2])

These operational inefficiencies represent **core opportunities for AI platforms**.

---

# Research Workflow

## Step 1 — Firm Overview

Collect basic firm information.

Fields:

* Founding year
* Headquarters
* Offices
* Assets under management (AUM)
* Number of employees
* Strategy (buyout, growth, private credit, multi-strategy)

Sources:

* Firm website
* Wikipedia
* financial media
* investor presentations

---

# Step 2 — Organizational Structure

Identify the **operating structure of the firm**.

Focus on departments relevant to AI adoption:

Key teams:

* Finance
* Investor relations
* Technology
* Data / AI
* Operations
* Portfolio operations

Create a structure map:

```
CEO / Managing Partner
│
├ Investment Team
├ Portfolio Operations
├ Finance
├ Investor Relations
├ Technology / Data
└ Compliance / Risk
```

Determine:

* size of back office
* level of tech maturity
* whether they have a **data team or AI initiatives**

---

# Step 3 — Identify ICP (Ideal Customer Profiles)

Focus on **decision makers who influence AI adoption**.

Primary ICPs:

### CFO

Responsible for:

* fund reporting
* financial operations
* audit processes
* LP communications

AI relevance:

* LP reporting automation
* fund analytics
* compliance reporting
* financial workflow automation

---

### CTO / CIO

Responsible for:

* technology infrastructure
* internal systems
* integration of platforms

AI relevance:

* AI infrastructure
* data platforms
* system integrations

---

### Head of Data / AI / Quant

Responsible for:

* analytics
* AI implementation
* data pipelines
* reporting systems

---

### Head of Investor Relations

Responsible for:

* LP communications
* investor reporting
* fund updates
* capital raising

---

For each ICP collect:

```
Name
Title
Background
LinkedIn
Previous firms
Education
Public interviews or quotes
```

---

# Step 4 — LP Base Analysis

Understanding LPs helps explain **why the firm must improve reporting and analytics**.

Identify LP categories:

* pension funds
* sovereign wealth funds
* endowments
* insurance companies
* family offices
* fund-of-funds

Research sources:

* fund prospectuses
* press releases
* investor lists
* news articles

Analyze:

```
LP types
Institutional size
Reporting expectations
Transparency requirements
```

Why this matters:

LPs increasingly demand:

* more granular performance data
* faster reporting
* better transparency. ([henon.ai][2])

This creates **strong incentives for AI-driven reporting systems**.

---

# Step 5 — Operational Pain Points

Identify areas where AI can create value.

Common industry pain points:

### LP reporting

Problems:

* manual compilation of reports
* fragmented portfolio data
* slow quarterly reporting cycles

Many firms spend **500-700 hours per quarter** preparing investor reporting for large funds. ([Acquis Consulting][1])

---

### Portfolio monitoring

Problems:

* data collected from many portfolio companies
* inconsistent formats
* slow analytics.

---

### Audit readiness

Problems:

* documentation scattered across systems
* compliance processes manual
* lack of audit trails.

AI can create **audit-ready reporting and structured financial data extraction**. ([73 Strings][3])

---

### Data silos

Many firms struggle with **fragmented data across CRM, portfolio systems, and reporting tools**. ([LinkedIn][4])

---

# Step 6 — Technology Stack

Identify existing tools.

Common platforms:

* Juniper Square
* iLEVEL
* DealCloud
* Salesforce
* Tableau
* Excel-heavy workflows

Look for signals:

* hiring data engineers
* AI strategy announcements
* analytics platform adoption

---

# Step 7 — Events and Conferences

Identify **events attended by leadership or IR teams**.

Examples of relevant event types:

* private capital conferences
* LP/GP meetings
* fintech and AI conferences
* investor relations forums

Research:

```
conference speaking engagements
panel participation
industry association memberships
```

Goal:

Find **events where outreach or networking is possible**.

---

# Step 8 — Content and Thought Leadership

Identify what topics the firm talks about.

Sources:

* podcasts
* conference talks
* blog posts
* whitepapers
* LinkedIn posts

Look for keywords:

* AI
* data analytics
* reporting transparency
* portfolio monitoring
* operational efficiency

---

# Step 9 — Hiring Signals

Hiring is a strong signal of **technology priorities**.

Search for roles such as:

* Head of Data
* AI Engineer
* Data Platform Lead
* Reporting Automation Lead
* Portfolio Analytics Manager

These indicate **internal AI initiatives**.

---

# Step 10 — Personalized GTM Strategy

Using the research, generate a **custom outreach strategy**.

Include:

## Key Decision Makers

List:

* CFO
* CTO
* Head of Data
* Head of Investor Relations

---

## AI Opportunity Hypothesis

Example:

```
This firm likely struggles with LP reporting across multiple funds and portfolio companies.

AI platform could automate:
- portfolio data aggregation
- LP report generation
- audit documentation
- investor dashboards
```

---

## Outreach Angles

### Email angle

Example:

```
Subject: AI for LP reporting at [Firm]

Noticed your firm manages [X] funds and works with institutional LPs.

Many PE firms we work with spend hundreds of hours per quarter assembling LP reports.

Our AI platform aggregates portfolio data automatically and generates investor-ready reporting in minutes.
```

---

### Event targeting

List events where outreach is possible.

Example:

```
SuperReturn
IPEM
Milken Global Conference
Private Equity International events
```

---

### Content hook

Reference something specific:

* a recent deal
* a new fund
* an LP announcement

---

# Final Output Format

```
# AI Sales Research: [Firm Name]

## Firm Overview

## Organizational Structure

## Key Decision Makers (ICP)
CFO
CTO
Head of Data
Head of Investor Relations

## LP Base

## Operational Pain Points

## Technology Stack

## Events and Conferences

## Hiring Signals

## AI Opportunity Hypothesis

## Personalized GTM Strategy
Email angle
Event outreach
Conversation hooks

