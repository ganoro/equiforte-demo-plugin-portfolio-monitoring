---
name: geopolitical-report
description: Analyze how a geopolitical event impacts portfolio MOIC and identify opportunities to boost absolute returns — produces a CFO-ready presentation with MOIC impact estimates and data collection recommendations
tags:
  - geopolitical
  - moic
  - risk
  - portfolio
  - opportunity
  - presentation
placeholder: "e.g. How will the Iran-US conflict impact MOIC across Fund IV portfolio companies?"
defaultOutput: File
icon: IconWorld
arguments:
  - name: event
    description: "The geopolitical event or dynamic to analyze (e.g. 'Iran-US conflict', 'EU CBAM', 'Red Sea disruption')"
    required: true
  - name: scope
    description: "Fund name, GP name with URL, or portfolio company list (default: all workspace portfolio companies)"
    required: false
---

# /geopolitical-report — Geopolitical MOIC Impact Analysis

Produce a CFO-ready presentation analyzing how a specific geopolitical event impacts MOIC (Multiple on Invested Capital) across portfolio companies, and what data to collect to unlock further value.

## Target

**Event**: $ARGUMENTS

## Instructions

### Step 1 — Initialize & Build Portfolio Registry (max 3 tool calls)

1. Run `mkdir -p output _research/geopolitical`.
2. Scan workspace files for portfolio data (tear sheets, financial reports).
3. If a GP URL is provided, fetch the portfolio page in ONE call to get all companies at once — do NOT fetch individual company pages.
4. Build a **Portfolio Registry** with available data:

| # | Company | Sector | Key Products/Services | Invested Capital | Current Value | MOIC (if known) |
|---|---------|--------|-----------------------|-----------------|---------------|-----------------|

5. Write to `_research/geopolitical/portfolio-registry.md`.

**Budget guard**: Complete this step in 3 tool calls max (1 file scan + 1 web fetch + 1 write).

### Step 2 — Assess Geopolitical Event & Sector Impact (max 3 tool calls)

1. Run 1-2 web searches on the geopolitical event — focus on **sector-level impacts** (not per-company):
   - Search: `"[event]" impact [top sectors in portfolio] manufacturing industrial supply chain [year]`
   - Search: `"[event]" opportunities reshoring nearshoring industrial [year]` (if relevant)
2. Synthesize into a **Sector Impact Map** — group portfolio companies by sector and assess:

| Sector | Companies | Risk Level (1-5) | Risk Driver (1 sentence) | Opportunity Level (0-4) | Opportunity Driver (1 sentence) |
|--------|-----------|-------------------|--------------------------|------------------------|---------------------------------|

3. Write to `_research/geopolitical/sector-impact.md`.

**Do NOT research each company individually.** Group by sector and apply sector-level findings.

### Step 3 — MOIC Impact Analysis (no additional tool calls needed)

For each portfolio company, estimate the MOIC impact using the MOIC framework and sensitivity formula from the `geopolitical-report` skill.

Produce a **MOIC Impact Table**:

| Company | Current MOIC (est.) | Base Case MOIC | Stress Case MOIC | MOIC Delta (Stress) | Opportunity MOIC | MOIC Delta (Upside) | Key Driver |
|---------|--------------------:|---------------:|-----------------:|--------------------:|-----------------:|--------------------:|------------|

Where:
- **Base Case**: Current trajectory continues
- **Stress Case**: Event escalates — apply sector risk factor to current value
- **Opportunity MOIC**: Company captures geopolitical upside (nearshoring, pricing power, competitive displacement)

Also compute **Portfolio-Level MOIC** (weighted by invested capital) for each scenario.

Write to `_research/geopolitical/moic-impact.md`.

### Step 4 — Data Collection Recommendations (no additional tool calls needed)

Using the `geopolitical-report` skill's data collection framework, produce:

1. **Immediate Data Requests** — what to ask portfolio companies NOW to quantify exposure:

| Data Point | Why It Matters | Which PortCos | Priority |
|-----------|----------------|---------------|----------|

2. **Ongoing Reporting Additions** — new KPIs to add to regular portco reporting:

| KPI | Definition | Frequency | MOIC Relevance |
|-----|-----------|-----------|----------------|

3. **Opportunity Intelligence** — data to collect to identify MOIC upside:

| Intelligence Need | How to Collect | Expected Insight |
|------------------|---------------|-----------------|

Write to `_research/geopolitical/data-collection.md`.

### Step 5 — Apply Branding & Generate Presentation

**Before generating any file**, read the design system and brand assets:

1. Read `/shared/plugins/{{PLUGIN_NAME}}/skills/design-system/references/tokens.md` — colors, typography, number formatting
2. Read `/shared/plugins/{{PLUGIN_NAME}}/skills/design-system/references/components.md` — title page, table, KPI card, chart patterns
3. Read `/shared/plugins/{{PLUGIN_NAME}}/skills/design-system/references/language.md` — PE/VC terminology, tone, disclaimers
4. Read `/shared/plugins/{{PLUGIN_NAME}}/brand/assets/brand-overrides.json` — firm name, confidentiality notice, custom colors
5. Copy logo into workspace: `cp /shared/plugins/{{PLUGIN_NAME}}/brand/assets/logo.png ./logo.png 2>/dev/null || true`

Apply the brand throughout:
- **Title slide**: Use firm name from `brand-overrides.json`, include logo, apply `primary` color (`#1B3A5C`) to header bar
- **Every slide footer**: Include confidentiality notice from `brand-overrides.json` + as-of date
- **Color tokens**: Use `primary` for headers, `positive`/`negative`/`warning`/`critical` for MOIC deltas and risk scores
- **Typography**: Calibri throughout per design-system tokens

Build the PPTX using the `pptx-generator` skill. If not available, generate directly using pptxgenjs or python-pptx with the brand tokens above.

**Slide Deck (8-10 slides max):**

| # | Title | Content |
|---|-------|---------|
| 1 | Title | "[Event] — Portfolio MOIC Impact Assessment" + date + CONFIDENTIAL |
| 2 | Executive Summary | 5 bullets: top MOIC risks, top opportunities, portfolio MOIC range, most affected companies, #1 urgent action |
| 3 | Portfolio Overview | Registry table from Step 1 |
| 4 | Sector Impact Map | Risk/opportunity by sector with color-coded scores from Step 2 |
| 5 | MOIC Impact Analysis | MOIC impact table from Step 3 — highlight companies with largest delta |
| 6 | Portfolio MOIC Scenarios | Bar/waterfall chart showing portfolio-level MOIC under Base/Stress/Opportunity |
| 7 | Top 3 Actions to Protect MOIC | Specific, actionable recommendations (company, action, cost, timeline) |
| 8 | Top 3 Actions to Boost MOIC | Geopolitical opportunities to increase returns |
| 9 | Data Collection Plan | What to start collecting from portcos now (from Step 4) |
| 10 | Caveats & Next Steps | Data gaps, confidence levels, recommended follow-up |

Save to `output/geopolitical-report.pptx`.

If DOCX is also requested, generate a companion document with the same content in narrative form. Save to `output/geopolitical-report.docx`.

## Critical Rules

- **MOIC is the central metric.** Every analysis must tie back to MOIC impact — not generic risk scores.
- **MOIC is time-agnostic** — it is an absolute return multiple (Total Value / Invested Capital), not annualized like IRR.
- **Budget discipline**: Complete in <=15 tool calls total. Group searches by sector, not by company.
- **Never fabricate data** — mark gaps as `[INSUFFICIENT DATA]` with ASSUMED confidence.
- **Every MOIC estimate must state**: basis (verified/estimated/assumed), what drives the delta, and the magnitude of impact.
- **Recommendations must be specific** — name the company, the action, the cost, and the MOIC impact.
- **State currency (USD) and as-of date** for all monetary values.
