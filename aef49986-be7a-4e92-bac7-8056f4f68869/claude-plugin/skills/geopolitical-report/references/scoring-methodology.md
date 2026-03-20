# Geopolitical Risk & Opportunity Scoring Methodology

## Risk Scoring (1-5 Scale)

| Score | Label | Definition | Color Code |
|-------|-------|------------|------------|
| 1 | **LOW** | No material exposure; stable environment | Green |
| 2 | **MODERATE** | Some exposure but manageable with existing controls | Yellow |
| 3 | **ELEVATED** | Material exposure requiring active monitoring and contingency planning | Orange |
| 4 | **HIGH** | Significant exposure with potential for near-term impact; mitigation needed | Red |
| 5 | **CRITICAL** | Imminent or active threat; immediate action required | Dark Red |

### Risk Dimensions Detail

#### 1. Supply-Chain Exposure
- Score 1: No suppliers or inputs from affected regions
- Score 2: <10% of COGS from affected regions, alternatives available
- Score 3: 10-30% of COGS from affected regions, alternatives exist but switching takes 3-6 months
- Score 4: 30-60% of COGS from affected regions, limited alternatives
- Score 5: >60% of COGS from affected regions, single-source critical inputs

#### 2. Market Access
- Score 1: No revenue from affected countries/regions
- Score 2: <5% of revenue from affected regions
- Score 3: 5-15% of revenue from affected regions
- Score 4: 15-30% of revenue, or affected region is a key growth market
- Score 5: >30% of revenue from affected regions, or entire business model depends on access

#### 3. Regulatory/Tariff
- Score 1: No tariff or regulatory exposure to the event
- Score 2: Minor tariffs (<2% of COGS), easily absorbed
- Score 3: Moderate tariffs (2-10% of COGS) or new compliance costs
- Score 4: Significant tariffs (>10% of COGS) or major compliance overhaul required
- Score 5: Prohibitive tariffs/regulations that fundamentally alter the business model

#### 4. Input Cost
- Score 1: Input costs unaffected by the event
- Score 2: <5% increase in key input costs, hedgeable
- Score 3: 5-15% increase in key inputs, partially hedgeable
- Score 4: 15-30% increase, difficult to hedge or pass through
- Score 5: >30% increase or critical input becomes unavailable

#### 5. Customer Impact
- Score 1: End-customer demand unaffected
- Score 2: Minor demand softening (<5%), temporary
- Score 3: Moderate demand impact (5-15%), may persist
- Score 4: Significant demand decline (15-30%) or customer base concentrated in affected region
- Score 5: Severe demand destruction (>30%) or customers directly sanctioned/restricted

## Opportunity Scoring (0-4 Scale)

| Score | Label | Definition |
|-------|-------|------------|
| 0 | **NONE** | No identifiable opportunity from this geopolitical dynamic |
| 1 | **LOW** | Marginal or speculative opportunity requiring significant assumptions |
| 2 | **MODERATE** | Tangible opportunity but requires investment, repositioning, or execution risk |
| 3 | **SIGNIFICANT** | Clear and actionable opportunity with favorable risk/reward profile |
| 4 | **HIGH** | Major strategic opportunity — potential step-change in competitive position or market share |

### No Double-Counting Rule

Each opportunity must represent a distinct mechanism. If nearshoring creates competitive advantage, score under Nearshoring only — do not also score under Competitive Displacement unless a separate, independent mechanism exists (e.g., a competitor is sanctioned independently of supply-chain trends).

## Composite Score Calculation

### Risk Composite
```
Composite_Risk = (SupplyChain + MarketAccess + Regulatory + InputCost + CustomerImpact) / 5
```

Equal weights by default. Adjust if portfolio is concentrated in sectors where specific dimensions dominate (e.g., increase Supply-Chain weight for manufacturing-heavy portfolios).

### Opportunity Composite
```
Composite_Opportunity = (Nearshoring + CompetitiveDisplacement + PricingPower + GovtIncentives) / 4
```

### MOIC Translation

To convert scores to MOIC impact estimates:

| Risk Score | Estimated Value Impact | MOIC Translation |
|-----------|----------------------|------------------|
| 1 | 0% impact | No MOIC change |
| 2 | 2-5% value at risk | -0.02x to -0.05x MOIC |
| 3 | 5-15% value at risk | -0.05x to -0.15x MOIC |
| 4 | 15-30% value at risk | -0.15x to -0.30x MOIC |
| 5 | 30-50%+ value at risk | -0.30x to -0.50x+ MOIC |

| Opportunity Score | Estimated Value Upside | MOIC Translation |
|------------------|----------------------|------------------|
| 0 | 0% upside | No MOIC change |
| 1 | 1-3% value creation | +0.01x to +0.03x MOIC |
| 2 | 3-10% value creation | +0.03x to +0.10x MOIC |
| 3 | 10-25% value creation | +0.10x to +0.25x MOIC |
| 4 | 25%+ value creation | +0.25x+ MOIC |

These are rough calibrations. Refine with actual financial data when available.
