---
name: acquisition-targets
description: Identify and screen potential acquisition or add-on targets for portfolio companies or new platform investments
tags:
  - acquisition
  - m-and-a
  - targets
  - screening
  - deal-sourcing
placeholder: "e.g. Find add-on targets for our healthcare services portco, or Screen software targets at 5-10x EBITDA"
defaultOutput: Document
icon: IconTargetArrow
arguments:
  - name: scope
    description: "Portfolio company (for add-ons), sector, or investment thesis for new platforms"
    required: true
  - name: parameters
    description: "Screening parameters (comma-separated). e.g. 'min revenue $20M, max EBITDA multiple 8x, US-based, recurring revenue >60%'"
    required: false
  - name: min_irr
    description: "Minimum IRR expectation (e.g. 20%). Default: fund target IRR"
    required: false
---

# /acquisition-targets — M&A Target Identification

Screen and evaluate potential acquisition targets — either add-on acquisitions for existing portfolio companies or new platform investments.

## Parameters

- **Scope**: $ARGUMENTS
- **Screening parameters**: (from arguments, if provided)
- **Min IRR**: (from arguments, default: fund target)

## Efficiency Rules (TARGET: 900 seconds)

- Max 8-10 web searches total — focus on sector databases and deal reports
- Don't deep-dive every target — surface 8-12 candidates, then rank
- Use available data only — don't try to build full financial models for each target
- One consolidated target list with scoring, not individual target reports

## Instructions

### Step 1 — Define Screening Criteria

Based on scope and parameters, establish:

| Criterion | Target Range | Weight | Source |
|-----------|-------------|--------|--------|
| Revenue | $X-$XM | X% | User/fund mandate |
| EBITDA Margin | >X% | X% | Sector benchmark |
| Growth Rate | >X% | X% | User/fund mandate |
| Geography | [regions] | X% | User/fund mandate |
| EV/EBITDA Multiple | X-Xx | X% | Market data |
| Revenue Quality | >X% recurring | X% | User/fund mandate |
| Customer Concentration | <X% top customer | X% | Risk threshold |

If user specifies min IRR expectations, back-solve for maximum entry multiple.

### Step 2 — Identify Candidates

Using web research and workspace data, identify 8-12 potential targets:

| # | Company | Sector/Sub-sector | Est. Revenue | Est. EBITDA | Est. EBITDA Margin | Geography | Key Differentiator | Source |
|---|---------|-------------------|-------------|------------|-------------------|-----------|--------------------|--------|

Sources: PitchBook, Crunchbase, industry reports, conference presentations, press releases.

### Step 3 — Strategic Fit Scoring

Score each candidate on strategic fit:

| Company | Revenue Synergy | Cost Synergy | Geographic Fit | Capability Add | Cultural Fit | Customer Overlap | Overall Fit Score |
|---------|----------------|-------------|----------------|----------------|--------------|-----------------|-------------------|

Scale: 1 (Low) to 5 (High)

### Step 4 — Preliminary Returns Analysis

For top 5 candidates, estimate returns at illustrative multiples:

| Company | Est. EBITDA | Entry Multiple | Entry EV | Equity Required | 5Y EBITDA (est.) | Exit Multiple | Exit EV | Gross MOIC | Gross IRR |
|---------|------------|----------------|---------|----------------|-----------------|---------------|---------|-----------|----------|

Show sensitivity: vary entry multiple and exit multiple.
Highlight which targets meet min IRR expectations.

### Step 5 — Risk Assessment

| Company | Key Risks | Customer Concentration | Regulatory Risk | Integration Complexity | Competitive Position |
|---------|----------|----------------------|----------------|----------------------|---------------------|

### Step 6 — Recommended Priority List

Rank targets by composite score:

| Rank | Company | Fit Score | Est. Returns | Risk Level | Recommended Action | Timeline |
|------|---------|-----------|-------------|------------|-------------------|----------|

Actions: Initiate outreach, Monitor, Research further, Pass

### Step 7 — Generate Output

Save to `output/acquisition-targets-[scope]-[date].docx`.
Include target summaries, scoring matrices, preliminary returns.
Offer XLSX with full screening data.

## Client Customization

- Users can overlay specific parameters: min IRR, max multiple, geography, sector
- Users can add/remove screening criteria
- Users can request deeper analysis on specific targets
- Scoring weights are adjustable

## Critical Rules

- Clearly label all financial estimates as ESTIMATED — these are not audited figures
- Source all company data to public information only
- Don't present screening results as investment recommendations
- Include standard disclaimer about preliminary nature of analysis
- Flag any targets where data quality is low
- Note if targets are currently in an auction or have known advisors

## Workspace Rules (MANDATORY)

1. Run `mkdir -p output _research` first
2. All deliverables to `output/` only
3. Use relative paths only
