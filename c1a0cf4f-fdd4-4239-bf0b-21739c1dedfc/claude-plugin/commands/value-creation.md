---
name: value-creation
description: Track and plan value creation across portfolio — decompose returns into revenue growth, margin expansion, multiple expansion, and leverage
tags:
  - value-creation
  - portfolio
  - returns
  - attribution
  - operating
placeholder: "e.g. Value creation analysis for Fund III, or Value creation plan for Acme Corp"
defaultOutput: Document
icon: IconTrendingUp
arguments:
  - name: target
    description: "Fund name, portfolio company, or 'all' for full portfolio"
    required: true
  - name: mode
    description: "Mode: track (historical attribution) or plan (forward-looking). Default: track"
    required: false
---

# /value-creation — Value Creation Tracking & Planning

Decompose and attribute value creation across the portfolio, or build forward-looking value creation plans.

## Parameters

- **Target**: $ARGUMENTS
- **Mode**: (from arguments, default: track)

## Efficiency Rules (TARGET: 900 seconds)

- Parse all financial data in one batch Python script
- Don't separately research each portco — use workspace data
- Limit web searches to 3 for sector benchmarks
- One consolidated output, not per-company reports

## Instructions

### Step 1 — Gather Investment Data

For each company in scope, extract:
- Entry date, entry valuation, entry EBITDA, entry revenue, entry multiple
- Current valuation, current EBITDA, current revenue, current multiple
- Debt at entry vs. current (for leverage effect)
- Capital invested (equity + follow-ons)

### Step 2 — Value Creation Bridge (Track Mode)

Decompose total value change into components:

| Component | Formula | $ Impact | % of Total |
|-----------|---------|----------|-----------|
| Revenue Growth | (Current Rev − Entry Rev) × Entry Margin × Entry Multiple | $X.XM | XX% |
| Margin Expansion | Entry Rev × (Current Margin − Entry Margin) × Entry Multiple | $X.XM | XX% |
| Multiple Expansion | Current EBITDA × (Current Multiple − Entry Multiple) | $X.XM | XX% |
| Leverage Effect | Debt Paydown × (1 − Tax Rate) | $X.XM | XX% |
| **Total Value Created** | Sum | **$X.XM** | **100%** |

### Step 3 — Company-Level Attribution

| Company | Entry Equity | Current Equity | Value Created | Rev Growth | Margin | Multiple | Leverage | MOIC |
|---------|-------------|----------------|--------------|------------|--------|----------|----------|------|

### Step 4 — Value Creation Levers Detail

For each company, identify the specific operational levers:

**Revenue Growth Drivers:**
- Organic growth (pricing, volume, new products/markets)
- Add-on acquisitions (revenue contribution, integration status)
- Cross-sell / up-sell initiatives

**Margin Improvement Drivers:**
- Procurement savings
- Operational efficiency (headcount optimization, automation)
- Revenue mix shift (higher-margin products/services)
- Pricing power

**Multiple Expansion Drivers:**
- Sector re-rating (public comp movement)
- Growth profile improvement
- Quality of earnings improvement
- Scale / size premium

### Step 5 — Forward Value Creation Plan (Plan Mode)

If mode = plan, build a 3-year value creation roadmap:

| Initiative | Category | Year 1 Impact | Year 2 Impact | Year 3 Impact | Cumulative | Owner | Status |
|-----------|----------|---------------|---------------|---------------|------------|-------|--------|

Map to exit scenarios:
- Base case exit MOIC and IRR
- Upside case (all initiatives succeed)
- Downside case (partial execution)

### Step 6 — Benchmarking

Compare value creation profile to:
- Fund-level targets and underwriting assumptions
- Industry benchmarks (Bain PE report, McKinsey PE value creation data)
- Prior fund value creation patterns

### Step 7 — Generate Output

Save to `output/value-creation-[target]-[date].docx`.
Include bridge charts, company-level detail, forward plans.
Offer PPTX for IC/board presentation, XLSX for detailed data.

## Critical Rules

- Value creation components must reconcile to total value change
- Entry metrics must match original underwriting/IC memo
- Current metrics must match latest reporting
- Specify whether multiples are EV/EBITDA, EV/Revenue, or other
- All assumptions in forward plans must be explicitly stated
- Don't conflate operational value creation with market/multiple tailwinds

## Workspace Rules (MANDATORY)

1. Run `mkdir -p output _research` first
2. All deliverables to `output/` only
3. Use relative paths only
