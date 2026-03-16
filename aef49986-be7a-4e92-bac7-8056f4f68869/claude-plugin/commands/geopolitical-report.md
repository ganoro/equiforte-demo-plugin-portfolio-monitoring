---
name: geopolitical-report
description: Generate a geopolitical risk & opportunity assessment across portfolio companies — analyzes supply chains, vendor exposure, country risk, sanctions, and macro events to produce a CFO-ready decision presentation
tags:
  - geopolitical
  - risk
  - supply-chain
  - portfolio
  - cfo
  - sanctions
  - vendor
  - opportunity
  - macro
  - presentation
placeholder: "e.g. Geopolitical risk assessment for Fund IV portfolio companies Q1 2026"
defaultOutput: File
icon: IconWorld
arguments:
  - name: scope
    description: "Fund name, portfolio company list, or 'all' for full portfolio (default: all workspace portfolio companies)"
    required: false
  - name: focus
    description: "Optional focus region or event (e.g. 'Taiwan Strait', 'EU CBAM', 'Red Sea disruption')"
    required: false
---

# /geopolitical-report — Geopolitical Risk & Opportunity Assessment

Produce a single CFO-ready presentation that maps every portfolio company against geopolitical risk vectors and emerging opportunities — enabling personalized, company-by-company decisions.

## Target

**$ARGUMENTS** (default: all portfolio companies in the workspace)

## Instructions

### Step 1 — Initialize Workspace & Gather Portfolio Data

1. Run `mkdir -p output _research/geopolitical` to prepare the workspace.
2. Scan the workspace for portfolio company data: financial statements, operating reports, vendor lists, supply-chain documentation, org charts, and prior research files.
3. Use the `document-parser` skill for PDF/XLSX/DOCX files.
4. Build the **Portfolio Company Registry** — one row per company:

| # | Company Name | Sector | HQ Country | Status | Investment Date | Current Valuation (USD) | Ownership (%) | Key Products/Services |
|---|-------------|--------|-----------|--------|-----------------|------------------------|---------------|----------------------|

5. Write the registry to `_research/geopolitical/portfolio-registry.md`.
6. If no portfolio data is found in the workspace, inform the user and ask them to provide a company list or upload documents.

### Step 2 — Map Supply Chains & Vendor Networks

For each portfolio company, extract or construct the **supply-chain and vendor map**:

1. Parse procurement records, vendor agreements, supplier lists, and BOM (bill of materials) data.
2. For each company, produce a **Vendor Exposure Table**:

| Company | Vendor/Supplier | Category | Country | Region | Revenue Dependency (%) | Single-Source? | Contract Expiry | Alt. Supplier Available? |
|---------|----------------|----------|---------|--------|----------------------|----------------|-----------------|-------------------------|

3. Produce a **Geographic Concentration Summary**:

| Country | # Vendors | % of Total Spend | # PortCos Exposed | Critical Dependency? |
|---------|-----------|------------------|--------------------|---------------------|

4. Flag **single points of failure** — any vendor that is sole-source for a critical input across one or more portfolio companies.
5. Write to `_research/geopolitical/supply-chain-map.md`.

### Step 3 — Identify Geopolitical Risk Vectors

Use the `geopolitical-report` skill to assess risks. For each portfolio company, evaluate these **risk dimensions**:

1. **Country/Sovereign Risk** — political stability, rule of law, expropriation risk for every country in the supply chain and revenue footprint.
2. **Sanctions & Trade Restrictions** — exposure to current or imminent sanctions regimes (OFAC SDN, EU, UK, UN), export controls (EAR/ITAR), and entity-list risks.
3. **Supply-Chain Disruption** — chokepoint exposure (straits, canals, ports), logistics fragility, raw-material concentration.
4. **Regulatory & Policy Risk** — tariffs, CBAM, data-localization mandates, ESG disclosure requirements, tax-regime changes.
5. **Conflict & Instability** — proximity to active or frozen conflicts, terrorism risk, civil unrest potential.
6. **Currency & Capital Controls** — FX volatility, repatriation restrictions, capital-account controls.
7. **Cyber & Technology Risk** — state-sponsored cyber threats, IP theft exposure, technology-transfer restrictions.

Produce a **Risk Vector Matrix** — one row per company, one column per risk dimension:

| Company | Country Risk | Sanctions | Supply-Chain | Regulatory | Conflict | Currency | Cyber/Tech | Composite Score |
|---------|-------------|-----------|-------------|------------|----------|----------|-----------|-----------------|

Score each cell: **LOW (1)** / **MODERATE (2)** / **ELEVATED (3)** / **HIGH (4)** / **CRITICAL (5)**.

Composite Score = weighted average (weights defined in the `geopolitical-report` skill).

Write to `_research/geopolitical/risk-matrix.md`.

### Step 4 — Identify Opportunities

Not all geopolitical shifts are negative. For each company, assess **opportunity vectors**:

1. **Nearshoring/Friendshoring** — can the company benefit from supply-chain relocation trends?
2. **Market Access** — do new trade agreements or diplomatic shifts open new markets?
3. **Competitive Displacement** — do sanctions or restrictions on competitors create market share opportunity?
4. **Pricing Power** — do tariffs or supply constraints give the company pricing leverage?
5. **Government Incentives** — does the company qualify for reshoring subsidies, tax credits, or strategic-sector support (e.g. CHIPS Act, IRA, EU Green Deal)?
6. **Resource Advantage** — does the company control or have preferential access to critical minerals, rare earths, or strategic inputs?

Produce an **Opportunity Vector Matrix**:

| Company | Nearshoring | Market Access | Competitive Displacement | Pricing Power | Govt. Incentives | Resource Advantage | Composite Opportunity Score |
|---------|------------|---------------|-------------------------|---------------|-----------------|-------------------|---------------------------|

Score each cell: **NONE (0)** / **LOW (1)** / **MODERATE (2)** / **SIGNIFICANT (3)** / **HIGH (4)**.

Write to `_research/geopolitical/opportunity-matrix.md`.

### Step 5 — Generate Scenario Analysis

Define **3 geopolitical scenarios** relevant to the portfolio (or to the user's focus region/event):

| Scenario | Description | Probability | Time Horizon | Key Trigger |
|----------|-------------|-------------|--------------|-------------|
| **Base Case** | Current trajectory continues with incremental changes | — | 12 months | — |
| **Stress Case** | Specific escalation (e.g. conflict, sanctions expansion, trade war) | — | 6-12 months | — |
| **Tail Risk** | Severe disruption (e.g. full decoupling, armed conflict, systemic sanctions) | — | 3-6 months | — |

For each scenario, estimate the **portfolio-level impact**:

| Scenario | Revenue at Risk (USD) | Revenue at Risk (% of Total) | EBITDA Impact (USD) | NAV Impact (%) | Most Affected PortCos |
|----------|----------------------|------------------------------|--------------------|-----------------|-----------------------|

Write to `_research/geopolitical/scenario-analysis.md`.

### Step 6 — Formulate CFO Decision Recommendations

For each portfolio company, produce a **personalized action card**:

| Field | Content |
|-------|---------|
| **Company** | Name |
| **Risk Profile** | Composite risk score + top 2 risk drivers |
| **Opportunity Profile** | Composite opportunity score + top 2 opportunity drivers |
| **Recommended Actions** | 2-4 specific, prioritized actions (e.g. "Dual-source PCB supplier from Vietnam to reduce China concentration from 85% to 40%") |
| **Timeline** | Immediate / 30 days / 90 days / 6 months |
| **Cost Estimate** | Rough order of magnitude for recommended actions |
| **Decision Required** | Yes/No — what the CFO needs to approve |

Write all action cards to `_research/geopolitical/action-cards.md`.

### Step 7 — Assemble CFO Presentation (PPTX)

Build a single PPTX presentation using the `pptx-generator` skill and the `design-system` skill. Follow the design tokens and component patterns.

**Slide Deck Structure:**

| Slide # | Title | Content |
|---------|-------|---------|
| 1 | Title Slide | "Geopolitical Risk & Opportunity Assessment — [Fund/Portfolio Name]" + as-of date + CONFIDENTIAL |
| 2 | Executive Summary | 5 bullet points: top risks, top opportunities, most exposed companies, recommended urgent actions, portfolio-level impact estimate |
| 3 | Portfolio Overview | Portfolio Company Registry table (from Step 1) |
| 4 | Geographic Exposure Map | Geographic Concentration Summary (from Step 2) — heatmap or table showing country exposure |
| 5 | Supply-Chain Vulnerability | Top 10 single-source/critical vendor dependencies (from Step 2) |
| 6 | Risk Vector Matrix | Full risk matrix with color-coded cells (GREEN/YELLOW/ORANGE/RED/DARK RED) per score (from Step 3) |
| 7 | Opportunity Vector Matrix | Full opportunity matrix with color-coded cells (from Step 4) |
| 8 | Scenario Analysis | Three-scenario table with portfolio impact estimates (from Step 5) |
| 9-N | Company Action Cards | One slide per portfolio company with the personalized action card (from Step 6) — highest-risk companies first |
| N+1 | Portfolio-Level Recommendations | Cross-cutting recommendations (e.g. portfolio-wide hedging, insurance, diversification mandates) |
| N+2 | Data Gaps & Caveats | Missing data, assumptions made, confidence levels, recommended follow-up research |
| N+3 | Appendix: Methodology | Scoring methodology, risk dimension weights, data sources |

Save the presentation to `output/geopolitical-report.pptx`.

### Step 8 — Validate & Deliver

1. Verify the PPTX file exists and is non-zero size.
2. Cross-check that every portfolio company appears in both the risk matrix and opportunity matrix.
3. Verify that all scores are within defined ranges (Risk: 1-5, Opportunity: 0-4).
4. Confirm every recommended action has a timeline and cost estimate.
5. Present a summary to the user:
   - Total companies assessed
   - Highest-risk companies (top 3)
   - Highest-opportunity companies (top 3)
   - Number of urgent decisions required
   - File path: `output/geopolitical-report.pptx`

## Critical Rules

- **Never fabricate geopolitical intelligence.** If a risk cannot be assessed from available data, mark it as `[INSUFFICIENT DATA]` with a confidence level of ASSUMED and flag it as a gap.
- **Every risk score must have a rationale** — a 1-2 sentence justification citing the underlying factor (e.g. "Score 4: 72% of revenue from Country X which is under active EU sanctions review per [source]").
- **All monetary figures must state currency (USD), as-of date, and gross/net where applicable.**
- **Recommendations must be specific and actionable** — not generic advice like "monitor the situation." Each action must name the company, the risk, and the concrete step.
- **Scenarios must be internally consistent** — if Stress Case assumes sanctions on Country X, every company with Country X exposure must show impact.
- **Opportunity scores must not double-count** — if nearshoring benefits a company, that same benefit should not also appear as "competitive displacement" unless it is a genuinely distinct mechanism.
- **Sanctions data must reference the specific regime** — OFAC SDN, EU Consolidated List, UK Sanctions List, UN Security Council — never just "sanctions."
- **Supply-chain data must distinguish tiers** — Tier 1 (direct suppliers), Tier 2 (suppliers' suppliers), Tier 3+ where available.
- **Presentation must be self-contained** — a CFO should be able to read it without any other document and make decisions.
- **Confidence levels are mandatory** on all assessments: VERIFIED (from audited/official sources) / REPORTED (from company or third-party reports) / ESTIMATED (analyst judgment with stated basis) / ASSUMED (no direct data, clearly labeled).
