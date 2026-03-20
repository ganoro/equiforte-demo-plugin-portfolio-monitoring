---
name: geopolitical-report
description: "This skill should be used when the user asks to 'generate a geopolitical report', 'analyze geopolitical impact on MOIC', 'geopolitical risk assessment', 'how does [event] affect portfolio returns', 'MOIC impact analysis', 'geopolitical opportunity assessment', 'what data to collect from portcos', 'supply chain risk to MOIC', 'sanctions impact on returns', or 'tariff impact on portfolio'. Covers MOIC-focused risk/opportunity scoring, sector-level impact analysis, and data collection frameworks for PE/VC portfolios."
---

# Geopolitical MOIC Impact Assessment

Evaluate how geopolitical dynamics affect Multiple on Invested Capital (MOIC) across a PE/VC portfolio. MOIC is the central metric — all risk and opportunity analysis ties back to absolute return impact.

## MOIC as the Central Metric

MOIC is time-agnostic and measures absolute return:

```
MOIC = (Current Value + Realized Distributions) / Total Invested Capital
```

Unlike IRR, MOIC does not penalize for holding period. It answers: "For every $1 invested, how many dollars come back?"

### MOIC Impact Channels

Geopolitical events affect MOIC through three channels:

| Channel | How It Affects MOIC | Example |
|---------|-------------------|---------|
| **Value Destruction** | Reduces current portfolio company value (numerator decreases) | Sanctions cut off a key market, reducing revenue and EV |
| **Value Creation** | Increases current value or creates new revenue (numerator increases) | Nearshoring trend drives new contracts to domestic manufacturer |
| **Cost Basis Change** | Additional capital required to navigate disruption (denominator increases) | Emergency supply chain restructuring requires follow-on investment |

### MOIC Sensitivity Formula

Estimate MOIC delta from a geopolitical event:

```
MOIC_stress = (Current_Value × (1 - Revenue_at_Risk% × Margin_Impact)) / Invested_Capital
MOIC_opportunity = (Current_Value × (1 + Revenue_Upside% × Margin_Capture)) / Invested_Capital
MOIC_delta = MOIC_stress - Current_MOIC  (for risk)
MOIC_delta = MOIC_opportunity - Current_MOIC  (for upside)
```

Where:
- **Revenue_at_Risk%**: Portion of revenue exposed to the geopolitical event (by sector/geography)
- **Margin_Impact**: How much of the affected revenue translates to value loss (0.0 to 1.0)
- **Revenue_Upside%**: New revenue opportunity from geopolitical shift
- **Margin_Capture**: Likelihood and margin on the upside opportunity

---

## Sector-Level Analysis (Not Per-Company)

Analyze geopolitical impact at the **sector level**, then apply to individual companies. This is faster and more accurate than per-company web research.

### Sector Risk Assessment

Score each sector on 5 risk dimensions (1-5 scale):

| Dimension | What to Assess |
|-----------|---------------|
| **Supply-Chain Exposure** | Raw materials, components, or logistics routes affected by the event |
| **Market Access** | Revenue from countries/regions directly affected |
| **Regulatory/Tariff** | New tariffs, export controls, or compliance costs |
| **Input Cost** | Energy, commodities, or labor cost increases |
| **Customer Impact** | End-customer demand affected by the event |

Composite Risk = average of the 5 scores. Apply to all companies in that sector.

### Sector Opportunity Assessment

Score each sector on 4 opportunity dimensions (0-4 scale):

| Dimension | What to Assess |
|-----------|---------------|
| **Nearshoring/Reshoring** | Demand shift toward domestic or allied-country production |
| **Competitive Displacement** | Competitors sanctioned, restricted, or disrupted |
| **Pricing Power** | Supply constraints enabling price increases |
| **Government Incentives** | Subsidies, tax credits, or strategic-sector support |

### Scoring Rules

- Every score requires a 1-sentence rationale
- Use the **highest applicable score** within a dimension
- Same sector = same score unless company-specific factors justify a difference
- Score definitions: see `references/scoring-methodology.md`

---

## MOIC Impact Table

The core deliverable. For each company:

| Field | Definition |
|-------|-----------|
| **Current MOIC (est.)** | Best estimate from available data: (Current Value + Distributions) / Invested |
| **Base Case MOIC** | Current trajectory — no escalation |
| **Stress Case MOIC** | Event escalates — apply sector risk factor |
| **Opportunity MOIC** | Company captures geopolitical upside |
| **MOIC Delta (Stress)** | Stress - Current (negative = value at risk) |
| **MOIC Delta (Upside)** | Opportunity - Current (positive = value creation) |

Compute **Portfolio-Level MOIC** as weighted average (weight = invested capital per company / total invested).

---

## Data Collection Framework

Three categories of data to request from portfolio companies to unlock MOIC value in geopolitical contexts.

### 1. Immediate Exposure Data (Request Now)

| Data Point | Why It Matters for MOIC |
|-----------|------------------------|
| Revenue by country/region (top 10) | Quantifies market-access risk to numerator |
| Supplier list with country of origin (Tier 1) | Identifies supply-chain concentration risk |
| Customer concentration by geography | Revenue dependency on affected regions |
| Commodity/input cost breakdown | Quantifies input-cost risk channel |
| Existing hedging positions (FX, commodity) | Determines natural protection |
| Government contract revenue (if any) | May be protected or enhanced by geopolitics |
| Current inventory levels (weeks of supply) | Buffer against short-term disruption |

### 2. Ongoing Reporting KPIs (Add to Quarterly Reports)

| KPI | Definition | MOIC Relevance |
|-----|-----------|----------------|
| **Geographic Revenue HHI** | Herfindahl index of revenue by country | Concentration risk to MOIC numerator |
| **Supplier Country Concentration** | % of COGS from top 3 countries | Supply-chain risk to margins |
| **Tariff Exposure Rate** | % of COGS subject to tariffs/duties | Direct cost pressure on MOIC |
| **Nearshore Pipeline** | Value of new contracts from reshoring trends | Upside opportunity to MOIC |
| **Input Cost Index** | Weighted index of key input costs vs. baseline | Margin pressure tracking |
| **Pricing Pass-Through Rate** | % of cost increases passed to customers | Margin protection ability |
| **Contract Backlog Duration** | Months of contracted revenue | Revenue visibility and MOIC floor |

### 3. Opportunity Intelligence (Collect to Identify MOIC Upside)

| Intelligence | How to Collect | Expected MOIC Insight |
|-------------|---------------|----------------------|
| Competitor supply-chain disruptions | Sales team intel, industry reports | Market share capture opportunity |
| Customer RFQs citing supply security | Track RFQ reasons in CRM | Demand shift quantification |
| Government incentive eligibility | Policy team review, trade counsel | Subsidy-driven margin expansion |
| Capacity utilization headroom | Ops team reporting | Ability to capture demand shift |
| New market entry barriers falling | BD team assessment | Geographic expansion opportunity |

---

## Presentation Standards & Branding

Before generating any output file, apply the firm's branding:

1. Read the `design-system` skill references (tokens, components, language) for visual standards
2. Read `brand/assets/brand-overrides.json` for firm name, custom colors, and confidentiality notice
3. Copy `brand/assets/logo.png` into the workspace and place on the title slide
4. Apply `primary` color from brand-overrides (default `#1B3A5C`) to all header bars and table headers
5. Include the confidentiality notice from brand-overrides on every slide footer

### MOIC-Specific Formatting

- **MOIC is the headline metric** on every analytical slide
- Color-code MOIC deltas using design-system tokens: `negative` (red) for downside, `positive` (green) for upside, `neutral` (grey) for no change
- Use `warning` (orange) for ELEVATED risk scores, `critical` (dark red) for CRITICAL
- Show portfolio-level MOIC in Base / Stress / Opportunity as a bar or waterfall chart
- Order companies by MOIC delta magnitude (largest impact first)
- Mark every estimate with confidence level: VERIFIED / ESTIMATED / ASSUMED
- State currency (USD) and as-of date on every slide

---

## Budget Discipline

This skill is designed to complete within tight turn/budget constraints:

1. **Batch by sector, not by company** — one web search per sector, not per company
2. **Max 5 web searches total** — event overview (1-2), sector impacts (2-3)
3. **Use the tear sheet/workspace data first** — only search for what is missing
4. **Skip supply-chain vendor mapping** unless vendor lists are in the workspace files
5. **Skip sanctions screening** — flag as a gap and recommend legal review instead

---

## Common Pitfalls

| Pitfall | Why It Fails | Fix |
|---------|-------------|-----|
| Researching each company individually | Burns all turns on data gathering, never reaches analysis | Group by sector, apply sector findings |
| Generic risk scores without MOIC tie-in | CFO cannot act on "Risk Level: 3" | Always show MOIC delta in dollars and multiples |
| Supply-chain mapping from web research | Data is rarely public, wastes turns | Use workspace files or flag as data gap |
| "Monitor the situation" recommendations | Not actionable | Name company, action, cost, timeline, MOIC impact |

---

## Additional Resources

### Reference Files

- **`references/scoring-methodology.md`** — Detailed 1-5 risk and 0-4 opportunity scoring definitions, weights, and calibration guidance
- **`references/sanctions-screening.md`** — Sanctions screening protocol (OFAC, EU, UK, UN) — recommend as follow-up, not inline analysis
- **`references/scenario-modeling.md`** — Three-scenario model construction, impact estimation formulas, and consistency rules
