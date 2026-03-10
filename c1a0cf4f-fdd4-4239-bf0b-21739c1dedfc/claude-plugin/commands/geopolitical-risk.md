---
name: geopolitical-risk
description: Assess geopolitical and macroeconomic risks impacting portfolio companies with weighted scoring and actionable mitigations
tags:
  - geopolitical
  - risk
  - macro
  - portfolio
  - geographic
placeholder: "e.g. Assess geopolitical risks for Fund III portfolio, or Analyze tariff impact on our manufacturing portcos"
defaultOutput: Document
icon: IconWorld
arguments:
  - name: scope
    description: "Fund, portfolio company, sector, or specific risk to analyze"
    required: true
  - name: factors
    description: "Additional risk factors to monitor (comma-separated). e.g. 'China tariffs, EU regulation, election impact'"
    required: false
---

# /geopolitical-risk — Geopolitical & Macro Risk Assessment

Produce a weighted geopolitical and macroeconomic risk assessment for the specified scope.

## Parameters

- **Scope**: $ARGUMENTS
- **Additional factors**: (from arguments, if provided)

## Efficiency Rules (TARGET: 900 seconds)

- Use web search for current geopolitical data — limit to 5-8 targeted searches
- Prioritize credible sources: Goldman Sachs, JP Morgan, IMF, World Bank, Economist Intelligence Unit
- Don't exhaustively research every country — focus on material exposures
- One combined analysis, not separate reports per risk

## Instructions

### Step 1 — Map Portfolio Geographic Exposure

Identify for each portfolio company:

| Company | HQ | Revenue Geography | Supply Chain Geographies | Employee Geographies | Key Regulatory Jurisdictions |
|---------|----|--------------------|--------------------------|---------------------|------------------------------|

### Step 2 — Identify Risk Factors

Scan for risks across these categories (plus any user-specified factors):

**Political & Regulatory:**
- Election cycles and policy changes (federal, state, local)
- Regulatory shifts (antitrust, data privacy, ESG mandates, trade policy)
- Tariffs and trade barriers
- Sanctions and export controls
- Zoning, permitting, and local government actions

**Macroeconomic:**
- Interest rate trajectory and central bank policy
- Inflation and wage pressure
- Currency movements
- Credit market conditions
- Recession probability

**Geopolitical:**
- Regional conflicts and instability
- Supply chain disruption risks
- Energy and commodity price volatility
- Technology decoupling (US/China/EU)

**Sector-Specific:**
- Industry regulation changes
- Competitive dynamics shifts
- Technology disruption
- Labor market conditions

### Step 3 — Score Each Risk (use `risk-weighting` skill)

For each identified risk, score with the following framework:

| Risk Factor | Category | Affected Portcos | Probability (1-10) | Severity (1-10) | Time Horizon | Weighted Score | Trend (↑↓→) |
|------------|----------|-----------------|--------------------|--------------------|--------------|---------------|-------------|

**Weighting formula**: Weighted Score = Probability × Severity × Exposure Factor
- Exposure Factor = % of portfolio NAV exposed to this risk (0.1 to 1.0)

**Allow client to adjust**: Note that weights, probabilities, and severity scores can be overridden. If the user specifies custom weights or factors, incorporate them and re-score.

### Step 4 — Geographic Risk Overlay

For each material geography, assess:

| Geography | Portcos Exposed | Political Risk | Economic Risk | Regulatory Risk | Overall Score | Key Events Next 12 Months |
|-----------|----------------|----------------|---------------|-----------------|---------------|---------------------------|

Include: elections, policy changes, zoning issues, local economic conditions.
Source from credible forecasts (EIU, Oxford Economics, Goldman Sachs).

### Step 5 — Scenario Analysis

Model 3 scenarios:

**Base Case** (60% probability): Current trajectory continues
**Upside** (20% probability): Favorable policy/market shifts
**Downside** (20% probability): Adverse geopolitical events materialize

For each scenario, estimate portfolio impact:
- NAV impact (% change by portco)
- Revenue impact
- Cost/margin impact
- Exit timeline impact

### Step 6 — Mitigation Playbook

For each high-scoring risk (Weighted Score ≥ 50), provide:

| Risk | Priority | Mitigation Action | Owner | Timeline | Cost Estimate | Residual Risk |
|------|----------|--------------------|-------|----------|--------------|---------------|

### Step 7 — Monitoring Dashboard

Create an ongoing monitoring framework:

| Risk Factor | Lead Indicator | Data Source | Trigger Threshold | Current Reading | Status |
|------------|----------------|-------------|-------------------|-----------------|--------|

### Step 8 — Generate Output

Save to `output/geopolitical-risk-[scope].docx`.
Include executive summary, full risk matrix, scenario analysis, mitigation playbook.
Offer PPTX for board presentation format.

## Adjustability

- Users can add custom risk factors at any time — incorporate and re-score
- Users can override probability/severity scores — recalculate weighted scores
- Users can set minimum IRR thresholds to filter which risks are material
- All parameters are adjustable on the fly — re-run with new inputs

## Critical Rules

- Source all geopolitical claims to credible institutions (named analyst/firm + date)
- Don't predict election outcomes — model scenarios for each outcome
- Don't overweight tail risks — use probability-weighted impact
- Include historical precedent where relevant ("In 2018, similar tariffs caused X")
- Flag when AI analysis relies on historical patterns vs. current intelligence
- State confidence levels on all assessments

## Workspace Rules (MANDATORY)

1. Run `mkdir -p output _research` first
2. All deliverables to `output/` only
3. Use relative paths only
