---
name: portfolio-monitor
description: Portfolio monitoring dashboard — track KPIs, flag outliers, compare to plan, and identify optimization opportunities across all portcos
tags:
  - portfolio
  - monitoring
  - optimization
  - kpi
  - dashboard
placeholder: "e.g. Portfolio review for Fund III, or Show me which portcos are underperforming plan"
defaultOutput: Spreadsheet
icon: IconLayoutDashboard
arguments:
  - name: fund
    description: Fund name or identifier (default: all funds)
    required: false
  - name: focus
    description: "Focus area: all, underperformers, outperformers, upcoming-exits, cash-flow"
    required: false
  - name: custom_kpis
    description: "Additional KPIs to track (comma-separated). e.g. 'customer churn, ARR growth, net retention'"
    required: false
---

# /portfolio-monitor — Portfolio Monitoring & Optimization

Generate a comprehensive portfolio monitoring dashboard with performance tracking, variance analysis, and optimization recommendations.

## Parameters

- **Fund**: $ARGUMENTS (default: all funds)
- **Focus**: (from arguments, default: all)
- **Custom KPIs**: (from arguments, if provided)

## Efficiency Rules (TARGET: 900 seconds)

- Parse all data files in one Python script
- Don't research each portco individually — batch process
- Limit web searches to 3-5 for market context
- Present findings in consolidated tables, not separate sections per company

## Instructions

### Step 1 — Portfolio Overview

Build a consolidated portfolio snapshot:

| Company | Sector | Vintage | Investment Cost | Current FV | MOIC | Revenue (LTM) | EBITDA (LTM) | EBITDA Margin | Revenue Growth YoY | Status |
|---------|--------|---------|----------------|------------|------|---------------|-------------|---------------|-------------------|--------|

Status: ● On Plan | ◐ Watch | ○ Underperforming | ★ Outperforming

### Step 2 — KPI Tracking vs. Plan

For each portfolio company, compare actuals vs. underwriting/budget:

| Company | KPI | Budget/Plan | Actual | Variance | Variance % | Trend (3Q) | Flag |
|---------|-----|-------------|--------|----------|-----------|------------|------|

Standard KPIs: Revenue, EBITDA, EBITDA Margin, Capex, Free Cash Flow, Leverage (Net Debt/EBITDA), Revenue Growth
Plus any custom KPIs specified by the user.

### Step 3 — Outlier Detection & Alerts

Flag companies that require attention:

**Underperformers** (any of):
- Revenue or EBITDA > 10% below plan
- EBITDA margin compression > 200bps
- Leverage ratio deteriorating
- Customer/revenue concentration increasing

**Outperformers** (any of):
- Revenue or EBITDA > 10% above plan
- Margin expansion > 200bps
- Accelerating growth
- Exit opportunity emerging

### Step 4 — Value Creation Attribution

For each company, decompose value creation (use `value-creation` skill):

| Company | Entry EBITDA | Current EBITDA | Revenue Growth | Margin Expansion | Multiple Expansion | Leverage Effect | Total Value Created |
|---------|-------------|----------------|----------------|------------------|--------------------|-----------------|--------------------|

### Step 5 — Public Comp Benchmarking

For each portco sector, show relevant public comparables (use `public-comps` skill):

| Public Comp | Ticker | EV/EBITDA | EV/Revenue | YTD Stock Performance | Implied Read-Through |
|-------------|--------|-----------|------------|----------------------|---------------------|

Note how public comp movements should inform portco marks.

### Step 6 — Cash Flow & Liquidity

| Company | Cash Balance | Revolver Availability | LTM FCF | Cash Runway (Months) | Next Debt Maturity | Covenant Headroom |
|---------|-------------|----------------------|---------|---------------------|--------------------|--------------------|

### Step 7 — Optimization Recommendations

Based on the analysis, provide prioritized recommendations:

| Priority | Company | Recommendation | Expected Impact | Timeline | Resource Required |
|----------|---------|----------------|-----------------|----------|-------------------|

Categories: Revenue acceleration, Cost optimization, Add-on M&A, Capital structure, Exit preparation, Management changes

### Step 8 — Generate Output

Save to `output/portfolio-monitor-[fund]-[date].xlsx` with tabs:
- Summary Dashboard
- Company Detail
- KPI Tracking
- Value Creation
- Public Comps
- Cash Flow
- Recommendations

Offer PPTX for board presentation.

## Client Customization

- Users can add custom KPIs at any time — incorporate into tracking
- Users can set custom thresholds for outlier detection
- Users can overlay specific parameters (min IRR expectations, target sectors)
- All monitoring criteria are adjustable on the fly

## Critical Rules

- All metrics must have as-of dates
- Variance analysis must show both absolute and percentage
- Don't fabricate operational data — mark gaps
- Public comp data must cite source and date
- Value creation attribution must reconcile to total value change
- Flag any portco where data is stale (> 1 quarter old)

## Workspace Rules (MANDATORY)

1. Run `mkdir -p output _research` first
2. All deliverables to `output/` only
3. Use relative paths only
