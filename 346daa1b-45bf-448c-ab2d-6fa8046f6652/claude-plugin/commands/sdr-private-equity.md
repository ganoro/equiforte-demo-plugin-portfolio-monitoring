---
name: sdr-private-equity
description: Act as an AI SDR for private equity
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

Great — below is a **much more powerful version of the skill** designed to behave like an **AI SDR + market intelligence agent for selling AI platforms to private capital firms**.

This version adds:

* **CFO + AI decision-maker discovery**
* **LP mapping**
* **conference targeting**
* **email generation**
* **account prioritization**
* **signals for when a firm is ready to buy AI**

It is designed to produce **outbound-ready GTM intelligence**.

---

# SKILL.md

# Skill: AI SDR for Private Capital Firms

## Purpose

This skill conducts **deep sales intelligence research on private capital firms** (private equity, hedge funds, private credit, venture capital, asset managers) to support **selling an AI platform**.

The goal is to generate **highly personalized go-to-market strategies** by understanding:

* firm structure
* decision makers (CFO, CTO, Head of AI/Data)
* LP relationships
* reporting workflows
* events attended by executives
* operational inefficiencies where AI creates value

The output enables **targeted outbound campaigns** (email, LinkedIn, event outreach).

---

# Core Hypothesis

Private capital firms face **significant operational inefficiencies**, particularly in:

* LP reporting
* portfolio monitoring
* audit preparation
* fund analytics
* document processing

Many firms spend **500–700 hours per quarter preparing investor reports**, often due to fragmented systems and manual data reconciliation. ([Acquis Consulting][1])

AI can automate:

* portfolio company data extraction
* fund performance aggregation
* investor-ready reporting
* audit trails and compliance workflows.

AI systems can also extract KPIs from documents like board packs and financial PDFs and validate them automatically. ([untap.pe][2])

These operational problems are **core entry points for selling AI platforms**.

---

# Inputs

| Input               | Description                                                     | Required |
| ------------------- | --------------------------------------------------------------- | -------- |
| `firm_name`         | Target firm                                                     | Yes      |
| `firm_type`         | PE / hedge fund / VC / private credit / asset manager           | Optional |
| `region`            | Geography                                                       | Optional |
| `research_depth`    | quick / standard / deep                                         | Optional |
| `ai_use_case_focus` | LP reporting / operations / deal sourcing / portfolio analytics | Optional |

Example:

```
firm_name: Apollo Global Management
firm_type: private equity
research_depth: deep
ai_use_case_focus: LP reporting, audit automation
```

---

# Research Process

---

# Step 1 — Firm Intelligence

Collect basic information.

Fields:

* founding year
* headquarters
* offices
* assets under management
* number of employees
* investment strategy

Also identify:

* number of funds
* typical fund size
* portfolio company count

This helps estimate **operational complexity**.

---

# Step 2 — Organizational Mapping

Understand the **internal structure**.

Focus on teams involved in:

* finance
* technology
* investor relations
* data / analytics
* operations
* portfolio operations

Create a structure map:

```
Managing Partner / CEO
│
├ Investment Team
├ Portfolio Operations
├ Finance
│  └ CFO
├ Investor Relations
│  └ Head of IR
├ Technology
│  └ CTO / CIO
└ Data / AI
```

This helps identify **who owns reporting workflows**.

---

# Step 3 — Identify ICPs

The main targets are **executives responsible for operations and reporting**.

Primary ICPs:

### CFO

Responsible for:

* fund accounting
* audit readiness
* LP reporting
* financial infrastructure

AI value:

* automated reporting
* fund analytics
* audit-ready documentation

---

### CTO / CIO

Responsible for:

* technology infrastructure
* system integration
* data platforms

AI value:

* automation infrastructure
* workflow orchestration
* data pipelines

---

### Head of Data / AI

Responsible for:

* analytics
* ML adoption
* internal tools

AI value:

* data extraction
* automated insights
* predictive analytics.

---

### Head of Investor Relations

Responsible for:

* LP communication
* reporting
* fundraising.

AI value:

* automated investor reports
* dashboard generation
* investor data access.

---

For each ICP collect:

```
Name
Title
LinkedIn
Previous firms
Education
Interviews or public comments
```

---

# Step 4 — LP Mapping

Understanding LPs helps explain **reporting pressure**.

Identify:

LP types:

* pension funds
* sovereign wealth funds
* endowments
* insurance companies
* family offices
* fund-of-funds

LPs require **increasing transparency and frequent reporting**, pushing firms to improve reporting infrastructure. ([untap.pe][2])

Document:

```
LP types
Large known LPs
Reporting expectations
```

---

# Step 5 — Technology Stack

Identify tools used by the firm.

Examples:

* DealCloud
* Salesforce
* Juniper Square
* iLEVEL
* Tableau
* Excel-heavy reporting

Look for:

* data platform investments
* analytics teams
* cloud migration

These indicate **AI readiness**.

---

# Step 6 — Operational Pain Points

Identify areas where AI could deliver value.

Common pain points:

### LP Reporting

Challenges:

* manual reporting
* fragmented data
* delayed reports.

### Portfolio Monitoring

Challenges:

* inconsistent data across portfolio companies
* slow analytics.

### Compliance & Audit

Challenges:

* manual documentation
* compliance tracking.

AI can centralize data and generate **LP-ready insights automatically**. ([Brownloop][3])

---

# Step 7 — Hiring Signals

Hiring is a **strong signal of tech priorities**.

Look for roles:

* Head of Data
* AI Engineer
* Data Platform Lead
* Portfolio Analytics Manager
* Reporting Automation Lead

These suggest **AI adoption readiness**.

---

# Step 8 — Event Intelligence

Identify conferences where the firm participates.

Look for:

* speaking engagements
* panel appearances
* sponsorships.

Major private capital events include:

* SuperReturn
* IPEM
* Milken Global Conference
* Private Equity International events
* Sohn Conference

These are key places to **target outreach or networking**.

---

# Step 9 — Content & Thought Leadership

Research:

* podcasts
* blog posts
* LinkedIn posts
* conference presentations.

Look for themes like:

* data-driven investing
* portfolio analytics
* AI adoption
* operational efficiency.

---

# Step 10 — AI Opportunity Hypothesis

Based on research, define **how AI fits this firm**.

Example:

```
The firm operates multiple funds with dozens of portfolio companies.

This likely creates reporting complexity and manual data aggregation.

AI could automate:
- portfolio KPI extraction
- fund-level analytics
- LP reporting
- audit documentation
```

---

# Step 11 — Outreach Personalization

Generate messaging tailored to the firm.

### Email Hook

Example:

```
Subject: AI for LP reporting at [Firm]

Noticed your team manages [X] portfolio companies and multiple funds.

Many firms spend hundreds of hours per quarter preparing LP reports due to fragmented data systems.

Our AI platform automatically aggregates portfolio data and generates investor-ready reporting in minutes.
```

---

### Conversation Starter

Use something specific:

* recent fundraise
* new portfolio company
* hiring data roles
* conference participation.

---

### Event Targeting

List events where decision makers may attend.

Example:

```
SuperReturn International
IPEM Cannes
Milken Global Conference
```

---

# Step 12 — Account Scoring

Score each target based on **AI sales likelihood**.

Factors:

| Signal                   | Score |
| ------------------------ | ----- |
| Large AUM                | +     |
| Many portfolio companies | +     |
| Hiring data engineers    | +     |
| Active LP fundraising    | +     |
| Legacy tech stack        | +     |

High score = **priority account**.

---

# Output Format

```
# AI Sales Intelligence: [Firm]

## Firm Overview

## Organizational Structure

## Key Decision Makers
CFO
CTO
Head of Data
Head of Investor Relations

## LP Base

## Technology Stack

## Operational Pain Points

## Hiring Signals

## Events and Conferences

## AI Opportunity Hypothesis

## Personalized Outreach Strategy
Email angle
Conversation hooks
Event targeting

## Account Score

## Sources
```

---

# Expected Outcome

This skill produces **sales-ready intelligence** that enables:

* hyper-personalized cold outreach
* conference networking strategy
* targeted ICP engagement
* faster pipeline creation.

---

✅ If you'd like, I can also create **3 extremely powerful add-ons to this skill** used by top AI sales teams:

1️⃣ **Fundraising Signal Detector**
(finds when a PE firm just raised a fund → perfect moment to sell AI)

2️⃣ **LP Network Mapper**
(map which LPs invest across multiple funds → multi-account selling)

3️⃣ **Conference Attendee Hunter**
(automatically finds which partners attend specific PE conferences)

These dramatically increase **outbound conversion rates in private capital.**

[1]: https://www.acquisconsulting.com/our-thinking/how-ai-powered-portfolio-reporting-is-reshaping-private-equity-human-capital-equation/?utm_source=chatgpt.com "AI-Powered Portfolio Reporting in Private Equity - Acquis"
[2]: https://www.untap.pe/untap-updates/the-rise-of-ai-in-private-equity-reporting?utm_source=chatgpt.com "The Rise of AI in Private Equity Reporting"
[3]: https://www.brownloop.com/blog/ai-agents-for-private-equity/?utm_source=chatgpt.com "AI Agents in Private Equity: Use Cases & Benefits | Brownloop"
