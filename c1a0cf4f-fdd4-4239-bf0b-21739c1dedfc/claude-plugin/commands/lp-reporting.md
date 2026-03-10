---
name: lp-reporting
description: Generate LP reports with fund performance, portfolio updates, capital activity, and investor communications
tags:
  - lp
  - reporting
  - investor
  - quarterly
  - ilpa
placeholder: "e.g. Generate Q4 2025 LP report for Fund IV"
defaultOutput: Document
icon: IconReportAnalytics
arguments:
  - name: fund
    description: Fund name or identifier
    required: true
  - name: period
    description: "Reporting period (e.g. Q4 2025, FY 2025). Default: most recent quarter"
    required: false
  - name: format
    description: "Output format: docx, pptx, xlsx. Default: docx"
    required: false
---

# /lp-reporting — LP Report Generator

Generate a comprehensive, ILPA-aligned LP report for the specified fund and period.

## Parameters

- **Fund**: $ARGUMENTS
- **Period**: (from arguments or most recent quarter)
- **Format**: (from arguments or DOCX default)

## Efficiency Rules (TARGET: 900 seconds)

- Use Python (pandas/openpyxl) for ALL data parsing — never the Read tool for CSV/XLSX
- Single Glob call to find all workspace data files
- One combined Python script for parse + compute
- Maximum 1 intermediate file: `_research/parsed_data.json`

## Instructions

### Step 1 — Gather Fund Data

Scan workspace for quarterly reports, capital account statements, NAV reports, cash flow files. Parse using `document-parser` skill. Extract:

- Fund-level metrics (commitments, called, distributed, NAV)
- Portfolio company updates (revenue, EBITDA, valuation marks)
- Capital activity (calls, distributions) for the period
- Unrealized / realized gains

### Step 2 — Compute Fund Performance

Using the `fund-performance` skill, calculate:

| Metric | Value | Prior Period | Change | Confidence |
|--------|-------|-------------|--------|------------|
| Gross IRR | X.X% | X.X% | +/- bps | [level] |
| Net IRR | X.X% | X.X% | +/- bps | [level] |
| TVPI | X.Xx | X.Xx | +/- | [level] |
| DPI | X.Xx | X.Xx | +/- | [level] |
| RVPI | X.Xx | X.Xx | +/- | [level] |
| PME (vs. index) | X.Xx | X.Xx | +/- | [level] |

Cross-check: TVPI = DPI + RVPI.

### Step 3 — Capital Activity Summary

| Date | Type | Amount | Cumulative Called | % of Commitment |
|------|------|--------|-------------------|-----------------|

Include: capital calls, distributions, recallable amounts, remaining unfunded.

### Step 4 — Portfolio Company Summary

For each portfolio company, present:

| Company | Sector | Investment Date | Cost | Fair Value | MOIC | Status |
|---------|--------|----------------|------|------------|------|--------|

For each company include a 2-3 sentence operational update covering:
- Revenue/EBITDA trajectory
- Key milestones achieved or missed
- Near-term outlook

### Step 5 — Public Market Comparables Context

For each portfolio company or vertical, reference:
- Key public comps and their recent stock performance
- Relevant trading multiples (EV/EBITDA, EV/Revenue, P/E)
- How public comp movements affect portco marks
- Source attribution to credible analysts (Goldman, Morgan Stanley, JP Morgan, etc.)

### Step 6 — Risk & Opportunity Summary

Present a weighted risk/opportunity matrix (use `risk-weighting` skill):

| Risk/Opportunity | Category | Weight (1-10) | Probability | Impact | Weighted Score | Mitigation/Action |
|-----------------|----------|--------------|-------------|--------|---------------|-------------------|

Include geopolitical, market, operational, and regulatory factors.

### Step 7 — Action Items & Outlook

Provide:
- Key actions for the next quarter (ranked by urgency)
- Portfolio outlook with upside/downside scenarios
- Upcoming capital activity expectations
- LP communication recommendations

### Step 8 — Generate Output

Save to `output/lp-report-[fund]-[period].docx` (or requested format).
Apply design system tokens. Include:
- Cover page with fund name, period, confidentiality notice
- Table of contents
- All sections above
- Appendix with detailed company financials
- Sources & notes page with all data attributions

## Critical Rules

- Every metric must have an as-of date and confidence label
- All return figures must specify gross vs. net
- Currency must be stated on all monetary values
- Public comp data must cite the source and date
- Never fabricate performance data — mark gaps explicitly
- Cross-check TVPI = DPI + RVPI
- Include standard ILPA disclaimers

## Workspace Rules (MANDATORY)

1. Run `mkdir -p output _research` first
2. All deliverables to `output/` only
3. Use relative paths only
