---
name: geographic-risk
description: Analyze geographic and political risks impacting specific portfolio companies — elections, zoning, regulations, local economic factors
tags:
  - geographic
  - political
  - risk
  - elections
  - zoning
  - regulatory
placeholder: "e.g. Geographic risk for our Texas-based portcos given upcoming elections, or Zoning risk for our logistics portfolio"
defaultOutput: Document
icon: IconMapPin
arguments:
  - name: scope
    description: "Portfolio company, region, fund, or specific geographic risk to analyze"
    required: true
  - name: factors
    description: "Specific factors to evaluate (comma-separated). e.g. 'local elections, zoning changes, tax policy, labor laws'"
    required: false
---

# /geographic-risk — Geographic & Political Risk Analysis

Assess location-specific political, regulatory, and economic risks that may impact portfolio companies.

## Parameters

- **Scope**: $ARGUMENTS
- **Additional factors**: (from arguments, if provided)

## Efficiency Rules (TARGET: 600 seconds)

- Max 6-8 web searches — target specific geographies, not broad surveys
- Focus on material exposures only — skip geographies with <5% revenue exposure
- Consolidate findings into one risk matrix, not per-geography reports
- Use credible local/national sources, not general news aggregators

## Instructions

### Step 1 — Map Geographic Exposures

| Company | HQ State/Country | Revenue by Geography | Operations by Geography | Key Facilities | Regulatory Jurisdiction |
|---------|------------------|---------------------|------------------------|----------------|------------------------|

Flag concentrated exposures (>25% of revenue or operations in single jurisdiction).

### Step 2 — Political & Election Risk

| Geography | Upcoming Elections | Current Political Lean | Potential Policy Shifts | Impact on Portco | Probability | Severity |
|-----------|-------------------|----------------------|----------------------|-----------------|-------------|----------|

For each material election:
- Key candidates and their platform positions relevant to portcos
- Polling data and likely outcomes (cite source)
- Policy implications for each outcome (scenario A vs. B)
- Don't predict winners — model impact for each scenario

### Step 3 — Regulatory & Zoning Risk

| Geography | Regulatory Area | Current Status | Proposed Changes | Affected Portcos | Timeline | Impact Assessment |
|-----------|----------------|----------------|-----------------|-----------------|----------|-------------------|

Include: zoning changes, permitting requirements, environmental regulations, labor laws, tax policy changes, industry-specific regulations.

### Step 4 — Local Economic Factors

| Geography | GDP Growth | Unemployment | Wage Growth | Cost of Living Trend | Population Growth | Business Climate Rank | Key Economic Drivers |
|-----------|-----------|-------------|------------|---------------------|-------------------|---------------------|---------------------|

### Step 5 — Risk Scoring (use `risk-weighting` skill)

| Risk Factor | Geography | Portcos Affected | Probability (1-10) | Severity (1-10) | Exposure Factor | Weighted Score | Monitoring Trigger |
|------------|-----------|-----------------|--------------------|--------------------|-----------------|---------------|-------------------|

### Step 6 — Mitigation Strategies

For high-scoring risks (Weighted Score ≥ 40):

| Risk | Mitigation Option | Cost/Effort | Risk Reduction | Recommended Action | Timeline |
|------|-------------------|------------|----------------|-------------------|----------|

Options may include: geographic diversification, regulatory engagement, facility relocation, hedging, insurance, lobbying.

### Step 7 — Generate Output

Save to `output/geographic-risk-[scope]-[date].docx`.
Include risk maps, scoring matrices, mitigation plans.
Offer PPTX for board presentation.

## Critical Rules

- Source all political/regulatory claims to credible sources with dates
- Don't predict election outcomes — scenario model both/all outcomes
- Distinguish between enacted vs. proposed vs. speculative regulatory changes
- Include historical precedent where relevant
- State confidence levels on all assessments
- Flag when analysis relies on AI inference vs. published sources

## Workspace Rules (MANDATORY)

1. Run `mkdir -p output _research` first
2. All deliverables to `output/` only
3. Use relative paths only
