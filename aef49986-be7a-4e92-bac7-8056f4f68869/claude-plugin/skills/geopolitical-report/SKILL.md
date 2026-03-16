---
name: geopolitical-report
description: "Geopolitical risk and opportunity assessment methodology for PE/VC portfolio companies. Use this skill whenever a user mentions geopolitical risk, country risk, supply-chain risk, sanctions exposure, vendor concentration, trade war impact, tariff analysis, nearshoring, friendshoring, reshoring, political risk, sovereign risk, conflict exposure, export controls, OFAC, sanctions screening, or asks to assess how global events affect portfolio companies. Also triggers when a user wants to map supply chains, evaluate vendor dependencies, assess geographic concentration risk, or produce a risk/opportunity matrix for a CFO or investment committee. Covers: risk vector scoring, opportunity identification, scenario modeling, and CFO-ready decision frameworks."
---

# Geopolitical Risk & Opportunity Assessment

A structured methodology for evaluating how geopolitical dynamics — conflicts, sanctions, trade policy, regulatory shifts, and macro events — create risks and opportunities across a PE/VC portfolio. Designed to produce CFO-actionable intelligence, not academic analysis.

## When to Use This Skill

- Assessing geopolitical exposure across a portfolio or single company
- Mapping supply-chain and vendor concentration by country/region
- Screening for sanctions, export-control, or entity-list exposure
- Evaluating the impact of a specific geopolitical event on portfolio companies
- Producing risk/opportunity matrices for investment committee or CFO review
- Scenario modeling for trade wars, conflicts, regulatory shifts
- Identifying nearshoring, friendshoring, or reshoring opportunities

---

## Risk Assessment Framework

### The Seven Risk Dimensions

Every portfolio company is evaluated against seven geopolitical risk dimensions. Each dimension has specific indicators and data sources.

| # | Dimension | What It Measures | Key Indicators | Typical Sources |
|---|-----------|-----------------|----------------|-----------------|
| 1 | **Country/Sovereign Risk** | Political stability & institutional quality of countries in the company's footprint | Governance indices, regime type, transition risk, judicial independence, property rights | World Bank WGI, Economist Intelligence Unit, Freedom House, S&P sovereign ratings |
| 2 | **Sanctions & Trade Restrictions** | Exposure to current or imminent sanctions and export controls | OFAC SDN list, EU Consolidated List, UK Sanctions, UN SC resolutions, EAR/ITAR classification, Entity List | OFAC, EU, UK FCDO, BIS, company disclosures |
| 3 | **Supply-Chain Disruption** | Fragility of physical supply chain and logistics | Chokepoint dependency (Suez, Malacca, Panama, Hormuz, Bab el-Mandeb), port concentration, lead times, inventory buffers, raw-material sourcing | Company ops data, shipping indices (BDI, SCFI), commodity reports |
| 4 | **Regulatory & Policy Risk** | Exposure to tariffs, trade policy, and regulatory change | Tariff schedules, CBAM exposure, data-localization mandates, ESG disclosure rules, tax-regime changes, antitrust actions | WTO, USTR, European Commission, local regulators |
| 5 | **Conflict & Instability** | Proximity to armed conflict or civil unrest | Active conflicts, frozen conflicts, terrorism indices, protest/unrest trends, military buildup | ACLED, Uppsala Conflict Data, Global Terrorism Index, IISS |
| 6 | **Currency & Capital Controls** | FX volatility and repatriation risk | Currency volatility (30d/90d), capital-account restrictions, repatriation limits, dollarization trends | IMF AREAER, central bank policies, Bloomberg FX data |
| 7 | **Cyber & Technology Risk** | State-sponsored cyber threats and tech-transfer risk | APT group targeting, IP theft incidents, forced technology transfer, data sovereignty laws | CISA advisories, Mandiant/CrowdStrike threat intel, BIS tech controls |

### Scoring Methodology

Each risk dimension is scored on a 1-5 scale:

| Score | Label | Definition | Color Code |
|-------|-------|------------|------------|
| 1 | **LOW** | No material exposure; stable environment | Green |
| 2 | **MODERATE** | Some exposure but manageable with existing controls | Yellow |
| 3 | **ELEVATED** | Material exposure requiring active monitoring and contingency planning | Orange |
| 4 | **HIGH** | Significant exposure with potential for near-term impact; mitigation needed | Red |
| 5 | **CRITICAL** | Imminent or active threat; immediate action required | Dark Red |

### Composite Risk Score

The composite risk score is a **weighted average** of the seven dimensions:

```
Composite = (w1 × Country) + (w2 × Sanctions) + (w3 × SupplyChain) + (w4 × Regulatory) + (w5 × Conflict) + (w6 × Currency) + (w7 × Cyber)
```

**Default weights** (adjust based on portfolio characteristics):

| Dimension | Weight | Rationale |
|-----------|--------|-----------|
| Country/Sovereign Risk | 0.15 | Foundational but slow-moving |
| Sanctions & Trade | 0.20 | Binary impact — can halt operations overnight |
| Supply-Chain Disruption | 0.20 | Direct P&L impact for manufacturing/distribution |
| Regulatory & Policy | 0.15 | Affects margins and market access |
| Conflict & Instability | 0.10 | Severe but typically geographically contained |
| Currency & Capital | 0.10 | Manageable with hedging for most PE portfolios |
| Cyber & Technology | 0.10 | Growing but still probabilistic for most sectors |

**Total: 1.00**

Weights should be recalibrated if the portfolio is concentrated in sectors with different exposure profiles (e.g., increase Supply-Chain weight for manufacturing-heavy portfolios; increase Cyber weight for tech/SaaS portfolios).

### Scoring Rules

1. **Every score requires a rationale.** Never assign a score without 1-2 sentences explaining why (e.g., "Score 4: Company derives 68% of COGS from Tier 1 suppliers in [Country], which is subject to escalating EU sanctions review.").
2. **Scores must reflect current conditions** — not historical or hypothetical. State the as-of date.
3. **Use the highest applicable score** — if a company has both low and high risk in sub-categories of a dimension, the dimension score reflects the highest material risk.
4. **Cross-reference across companies** — the same country should receive consistent country-risk scores across all portfolio companies unless company-specific factors justify a difference.

---

## Opportunity Assessment Framework

### The Six Opportunity Dimensions

| # | Dimension | What It Measures | Indicators |
|---|-----------|-----------------|------------|
| 1 | **Nearshoring/Friendshoring** | Benefit from supply-chain relocation trends | Proximity to end-markets, wage competitiveness, FTA coverage, existing infrastructure |
| 2 | **Market Access** | New markets opened by trade agreements or diplomatic shifts | New FTAs, MFN status changes, bilateral investment treaties, diplomatic normalization |
| 3 | **Competitive Displacement** | Market share opportunity from competitors' geopolitical constraints | Competitor sanctions exposure, export-control impact on rivals, competitor supply-chain disruption |
| 4 | **Pricing Power** | Ability to pass through tariff/supply costs or benefit from scarcity | Market position, switching costs, product substitutability, tariff pass-through elasticity |
| 5 | **Government Incentives** | Eligibility for subsidies, tax credits, or strategic-sector support | CHIPS Act, IRA, EU Green Deal, national reshoring programs, special economic zones |
| 6 | **Resource Advantage** | Control over or preferential access to critical inputs | Critical mineral access, rare earth processing, strategic IP, technology leadership |

### Opportunity Scoring

| Score | Label | Definition |
|-------|-------|------------|
| 0 | **NONE** | No identifiable opportunity from geopolitical dynamics |
| 1 | **LOW** | Marginal or speculative opportunity |
| 2 | **MODERATE** | Tangible opportunity but requires investment or repositioning |
| 3 | **SIGNIFICANT** | Clear and actionable opportunity with favorable risk/reward |
| 4 | **HIGH** | Major strategic opportunity — potential step-change in competitive position |

### No Double-Counting Rule

Each opportunity must represent a **distinct mechanism**. If nearshoring creates a competitive advantage, score it under Nearshoring only — do not also score it under Competitive Displacement unless there is a separate, independent displacement mechanism (e.g., a competitor is sanctioned independently of supply-chain trends).

---

## Supply-Chain Mapping Methodology

### Tiered Vendor Analysis

Map supply chains at three tiers where data permits:

| Tier | Definition | Data Sources |
|------|-----------|-------------|
| **Tier 1** | Direct suppliers and vendors | Procurement records, AP ledger, vendor master, contracts |
| **Tier 2** | Suppliers' suppliers | Supplier audits, industry databases, SEC filings, sustainability reports |
| **Tier 3+** | Upstream raw-material and component sources | Industry reports, commodity research, government disclosures |

### Concentration Risk Metrics

Calculate for each portfolio company:

- **HHI (Herfindahl-Hirschman Index) by country**: Sum of squared market-share percentages of spend by country. HHI > 2,500 = highly concentrated.
- **Single-source ratio**: % of critical inputs with only one supplier.
- **Top-3 country concentration**: % of total spend in the top 3 countries.
- **Chokepoint exposure**: Number of logistics routes passing through identified chokepoints.

### Critical Dependency Flags

Flag any vendor/supplier relationship where ALL of the following apply:
1. Revenue dependency > 10% of COGS or > 5% of total revenue
2. Single-source (no qualified alternative supplier)
3. Located in a country scoring ≥ 3 on any risk dimension

---

## Sanctions Screening Protocol

### Step-by-Step Process

1. **Compile entity list**: All portfolio companies, their subsidiaries, directors, beneficial owners, and key vendors.
2. **Screen against**:
   - OFAC SDN List and Sectoral Sanctions (SSI)
   - EU Consolidated Financial Sanctions List
   - UK OFSI Consolidated List
   - UN Security Council Consolidated List
   - BIS Entity List, Denied Persons List, Unverified List
3. **Check secondary sanctions risk**: Even if not directly sanctioned, assess whether doing business with certain counterparties could trigger secondary sanctions (e.g., Iran/Russia secondary sanctions).
4. **Document results**: For each entity, record CLEAR / POTENTIAL MATCH / MATCH with specific list, entry date, and basis.
5. **Flag 50% ownership rule**: Under OFAC guidance, entities 50%+ owned by an SDN are themselves blocked, even if not individually listed.

### Sanctions Data Freshness

Sanctions lists change frequently. Always note:
- Date of last screening
- Which list versions were used
- Caveat that screening is point-in-time and not legal advice

---

## Scenario Modeling Framework

### Standard Three-Scenario Model

| Scenario | Probability Range | Description |
|----------|------------------|-------------|
| **Base Case** | 50-65% | Current geopolitical trajectory with incremental evolution |
| **Stress Case** | 20-35% | Specific escalation that materially disrupts one or more risk dimensions |
| **Tail Risk** | 5-15% | Severe, low-probability event with systemic portfolio impact |

### Scenario Construction Rules

1. **Each scenario must be internally consistent** — if you assume sanctions escalation, ALL companies with exposure must show impact.
2. **Quantify where possible** — estimate revenue-at-risk in USD, EBITDA impact, NAV impact.
3. **Identify triggers** — what observable event would signal a shift from Base to Stress or Stress to Tail.
4. **Time-bound** — every scenario has a time horizon (typically 3-12 months).
5. **Actionable** — each scenario should have associated hedging or mitigation actions.

### Impact Estimation

For each scenario × company combination, estimate:

```
Revenue at Risk = Affected Revenue Stream × Probability of Disruption × Severity Factor
EBITDA Impact = Revenue at Risk × Contribution Margin
NAV Impact = EBITDA Impact × Applicable Multiple
```

Where:
- **Severity Factor**: 0.0 (no impact) to 1.0 (complete loss)
- **Probability of Disruption**: Scenario-specific probability that this particular company is affected
- **Contribution Margin**: Company's incremental margin on the affected revenue

---

## CFO Decision Framework

### Action Card Structure

Every portfolio company action card must contain:

1. **Risk Profile Summary**: Composite score + top 2 risk drivers with rationale
2. **Opportunity Profile Summary**: Composite score + top 2 opportunity drivers
3. **Recommended Actions**: 2-4 specific actions ranked by urgency
4. **Decision Required**: Explicit Yes/No — what the CFO needs to approve
5. **Cost/Benefit Estimate**: Rough order of magnitude for each action
6. **Timeline**: Immediate / 30 days / 90 days / 6 months

### Action Specificity Standard

**BAD** (too generic):
- "Monitor geopolitical developments"
- "Consider diversifying supply chain"
- "Review sanctions compliance"

**GOOD** (specific and actionable):
- "Dual-source PCB assembly from Vietnam (Vendor: Foxconn VN) to reduce China concentration from 85% to 40% — est. $2.3M transition cost, 6-month timeline, requires board approval for CapEx"
- "Engage OFAC counsel to evaluate whether Subsidiary X's contract with [Entity] triggers secondary sanctions risk under Executive Order 14024 — est. $50K legal fee, 30-day turnaround"
- "File for CHIPS Act Section 48D tax credit on Austin fab expansion — est. $12M credit, application deadline Q3 2026, requires CFO sign-off on compliance attestation"

### Prioritization Logic

Rank recommended actions by:
1. **Urgency**: CRITICAL risks (score 5) → actions labeled "Immediate"
2. **Impact**: Higher revenue-at-risk → higher priority
3. **Feasibility**: Lower cost and shorter timeline → higher priority
4. **Reversibility**: Prefer reversible actions over irreversible commitments when uncertainty is high

---

## Presentation Standards

When producing the final PPTX deliverable:

1. Use the `design-system` skill for all visual formatting (tokens, components, language).
2. Use the `pptx-generator` skill for file creation.
3. Color-code all risk scores using the design-system color tokens:
   - LOW (1): `positive` token (green)
   - MODERATE (2): `accent` token (yellow/amber)
   - ELEVATED (3): `warning` token (orange)
   - HIGH (4): `negative` token (red)
   - CRITICAL (5): `critical` token (dark red)
4. Order company action-card slides from highest composite risk to lowest.
5. Include the methodology appendix so the CFO understands how scores were derived.
6. Mark every slide with as-of date and CONFIDENTIAL.

---

## Common Pitfalls

| Pitfall | Why It's Wrong | How to Avoid |
|---------|---------------|-------------|
| Treating all countries the same | China ≠ India ≠ Brazil — risk profiles differ enormously | Score each country independently on each dimension |
| Ignoring Tier 2+ suppliers | A Tier 1 supplier in "safe" country may source from "risky" country | Always attempt Tier 2 mapping; flag Tier 3 as a gap if unavailable |
| Conflating sanctions with country risk | A country can be high-risk without being sanctioned, and vice versa | Score Sanctions and Country Risk as separate dimensions |
| Static point-in-time view | Geopolitical risk is dynamic | State as-of date, recommend reassessment frequency (quarterly for PE) |
| Fabricating intelligence | No data ≠ no risk | Mark as `[INSUFFICIENT DATA]` with ASSUMED confidence; flag as gap |
| Generic recommendations | "Monitor the situation" is not actionable | Every recommendation must name the company, the risk, the action, the cost, and the timeline |
| Ignoring opportunities | Geopolitical shifts create winners, not just losers | Always complete the opportunity matrix — asymmetric returns come from upside, not just downside avoidance |

---

## Data Quality & Confidence

Apply the standard provenance framework from the ACSR lifecycle:

| Level | Label | Definition |
|-------|-------|------------|
| 1 | **VERIFIED** | From audited financial statements, official government registries, or direct company confirmation |
| 2 | **REPORTED** | From company management reports, third-party databases, or reputable news sources |
| 3 | **ESTIMATED** | Analyst judgment based on stated methodology and available data |
| 4 | **ASSUMED** | No direct data — assumption clearly labeled with basis and sensitivity |

Every risk score, opportunity score, and monetary estimate must carry a confidence label.
