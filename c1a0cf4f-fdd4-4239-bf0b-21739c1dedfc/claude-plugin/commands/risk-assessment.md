---
name: risk-assessment
description: Weighted risk and opportunity assessment with adjustable scoring, custom factors, and prioritized action plans
tags:
  - risk
  - opportunity
  - assessment
  - weighted
  - scoring
  - action-plan
placeholder: "e.g. Full risk/opportunity assessment for Fund III, or Risk assessment for our industrials portfolio"
defaultOutput: Document
icon: IconScale
arguments:
  - name: scope
    description: "Fund, portfolio company, sector, or specific topic"
    required: true
  - name: custom_factors
    description: "Additional factors to evaluate (comma-separated). e.g. 'supply chain China exposure, key man risk, customer concentration'"
    required: false
  - name: weights
    description: "Custom category weights (JSON). e.g. '{\"market\": 30, \"operational\": 25, \"financial\": 25, \"regulatory\": 20}'"
    required: false
---

# /risk-assessment — Weighted Risk & Opportunity Assessment

Produce a comprehensive, weighted risk and opportunity assessment with adjustable parameters and prioritized action plans.

## Parameters

- **Scope**: $ARGUMENTS
- **Custom factors**: (from arguments, if provided)
- **Custom weights**: (from arguments, or default weights below)

## Default Category Weights

| Category | Default Weight | Description |
|----------|---------------|-------------|
| Market & Competitive | 25% | Market dynamics, competitive position, sector trends |
| Operational | 25% | Management, execution, operational KPIs |
| Financial | 25% | Leverage, liquidity, cash flow, covenant compliance |
| Regulatory & Political | 15% | Regulatory changes, political risk, compliance |
| Strategic & Exit | 10% | Exit readiness, strategic positioning, M&A |

Users can override these weights at any time. Recalculate all scores when weights change.

## Efficiency Rules (TARGET: 900 seconds)

- Parse workspace data first, then supplement with 5-8 targeted web searches
- Score all risks in one pass — don't iterate
- Batch process companies, not one at a time
- One consolidated matrix, not separate assessments per company

## Instructions

### Step 1 — Risk Identification

Scan for risks across all categories. Include any user-specified custom factors.

For each risk, capture:

| # | Risk Factor | Category | Description | Affected Portcos | Source |
|---|------------|----------|-------------|-----------------|--------|

Minimum categories to cover:
- **Market**: demand shifts, pricing pressure, competitive entry, technology disruption, public comp performance
- **Operational**: key person dependency, supply chain, customer concentration, talent, technology
- **Financial**: leverage, liquidity, covenant compliance, refinancing risk, FX exposure
- **Regulatory**: new regulations, tax changes, ESG mandates, data privacy, industry-specific
- **Strategic**: exit market conditions, buyer universe, IPO window, holding period

### Step 2 — Opportunity Identification

Same framework for opportunities:

| # | Opportunity | Category | Description | Affected Portcos | Source |
|---|-----------|----------|-------------|-----------------|--------|

Include: add-on M&A, market expansion, pricing power, operational improvement, favorable regulation, public comp re-rating.

### Step 3 — Weighted Scoring (use `risk-weighting` skill)

Score each risk and opportunity:

| # | Factor | Type | Category | Probability (1-10) | Impact (1-10) | Category Weight | Weighted Score | Trend | Time Horizon |
|---|--------|------|----------|--------------------|--------------------|-----------------|---------------|-------|-------------|

**Weighted Score** = Probability × Impact × (Category Weight / 25)

This normalizes scores so a risk in a 25%-weighted category scores at face value, while a risk in a 10%-weighted category is scaled down.

### Step 4 — Risk/Opportunity Matrix

Plot on a 2×2 matrix:

**High Impact, High Probability** → Immediate action required
**High Impact, Low Probability** → Monitor closely, prepare contingency
**Low Impact, High Probability** → Manage operationally
**Low Impact, Low Probability** → Accept and monitor

### Step 5 — Action Plan with Timing Rationale (use `action-prioritization` skill)

For each action item, provide timing classification with explicit rationale:

| Action | Related Risk/Opp | Priority | Timing | Rationale for Timing | Owner | Resources | Success Metric |
|--------|-----------------|----------|--------|----------------------|-------|-----------|---------------|

**Timing Categories:**
- **Immediate** (0-30 days): Active threat to value, deteriorating fast, or time-sensitive opportunity. Explain why delay is costly.
- **Short-Term** (1-3 months): Important but not urgent. Can be planned and resourced. Explain dependencies.
- **Medium-Term** (3-12 months): Strategic initiatives. Explain why this timeframe is appropriate.
- **Long-Term** (12+ months): Structural changes, market-dependent actions. Explain what triggers acceleration.

### Step 6 — Sensitivity Analysis

Show how the risk profile changes under different assumptions:
- What if the top 3 risks all materialize simultaneously?
- What if the user changes category weights? (show impact of +/- 10% on top category)
- What is the aggregate portfolio impact under stress scenario?

### Step 7 — Monitoring Framework

| Risk/Opportunity | Lead Indicator | Data Source | Frequency | Trigger Threshold | Current Status |
|-----------------|----------------|-------------|-----------|-------------------|---------------|

### Step 8 — Generate Output

Save to `output/risk-assessment-[scope]-[date].docx`.
Include: executive summary, full scored matrix, 2×2 plot description, action plan, monitoring framework.
Offer PPTX for board presentation, XLSX for the detailed scoring data.

## Adjustability — Key Feature

This assessment is designed to be adjusted on the fly:

1. **Add factors**: User says "also consider X" → add to matrix, score, and re-rank
2. **Change weights**: User says "regulatory is more important" → adjust weight, recalculate all scores
3. **Override scores**: User says "I think this risk is higher" → update probability/impact, recalculate
4. **Add portco-specific risks**: User flags a risk the AI missed → incorporate immediately
5. **Set thresholds**: User says "only show risks above score X" → filter accordingly

Always confirm the adjustment and show the recalculated results.

## Critical Rules

- Every risk/opportunity must cite a source or rationale
- Scoring must be transparent — show the formula and inputs
- Action plan timing must include explicit rationale (not just "soon")
- Don't overwhelm — rank and present top 15-20 risks, top 10 opportunities
- Separate facts from opinions — label confidence levels
- Include both risks AND opportunities — this is not just a risk report
- Historical context: cite precedent where similar risks materialized

## Workspace Rules (MANDATORY)

1. Run `mkdir -p output _research` first
2. All deliverables to `output/` only
3. Use relative paths only
