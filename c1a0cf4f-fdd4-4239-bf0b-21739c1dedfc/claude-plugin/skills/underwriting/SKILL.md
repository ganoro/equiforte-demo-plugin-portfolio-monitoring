---
name: underwriting
description: >
  Real estate and PE/VC deal underwriting methodology — proforma modeling, NOI projection,
  cap rate analysis, debt sizing, return computation (IRR, equity multiple, cash-on-cash),
  sensitivity analysis, and risk scoring. Use this skill whenever a user mentions underwriting,
  proforma, deal analysis, acquisition modeling, NOI projection, cap rate, debt sizing, DSCR,
  levered/unlevered returns, exit cap rate, or investment recommendation. Also triggers on
  "should we buy this", "model the deal", "run the numbers", "what's the return", or any
  request to evaluate a real estate or PE acquisition.
---

# Underwriting — Deal Analysis Methodology

This skill provides the complete analytical framework for underwriting real estate acquisitions and PE/VC investments. It covers every quantitative discipline required to move from raw deal data to an investment recommendation.

## When to Use This Skill

- Building or reviewing a proforma (revenue + expense projection)
- Computing deal-level returns (IRR, equity multiple, cash-on-cash)
- Sizing debt and structuring the capital stack
- Running sensitivity or scenario analysis on a deal
- Scoring and ranking investment risks
- Producing a go/no-go investment recommendation

---

## 1. Core Formulas & Definitions

### Revenue Metrics

```
Gross Potential Rent (GPR) = Total Leasable SF × Market Rent/SF
Vacancy & Credit Loss    = GPR × Vacancy Rate (%)
Effective Gross Income   = GPR − Vacancy Loss + Other Income
```

### Net Operating Income (NOI)

```
NOI = Effective Gross Income (EGI) − Total Operating Expenses

Operating Expense Ratio = Total OpEx / EGI
NOI Margin = NOI / EGI
```

**Typical OpEx ratios by asset type (sanity check):**

| Asset Type | OpEx as % of EGI | Management Fee (% of EGI) |
|------------|-------------------|---------------------------|
| Office (Full Service) | 40–55% | 3–5% |
| Office (NNN) | 10–20% | 3–5% |
| Multifamily | 35–50% | 4–6% |
| Industrial | 15–25% | 3–4% |
| Retail (NNN) | 10–20% | 3–5% |
| Retail (Gross) | 35–50% | 4–6% |

### Capitalization Rate

```
Going-In Cap Rate = T-12 NOI / Purchase Price
Exit Cap Rate     = Forward NOI (Year N+1) / Gross Sale Price
Implied Value     = NOI / Cap Rate
```

**Critical**: Always use trailing-12-month NOI for going-in cap and **forward** (next year) NOI for exit cap. Never mix these.

### Debt Metrics

```
Loan-to-Value (LTV)           = Loan Amount / Property Value
Debt Yield                     = NOI / Loan Amount
Debt Service Coverage (DSCR)   = NOI / Annual Debt Service
Interest Coverage Ratio (ICR)  = NOI / Annual Interest Expense

Annual Debt Service (fixed-rate, amortizing):
  PMT = P × [r(1+r)^n] / [(1+r)^n − 1]
  where P = principal, r = monthly rate, n = total months
```

**Lender underwriting thresholds (typical):**

| Metric | Conservative | Moderate | Aggressive |
|--------|-------------|----------|------------|
| LTV | < 55% | 55–65% | 65–75% |
| DSCR | > 1.50x | 1.25–1.50x | 1.10–1.25x |
| Debt Yield | > 10% | 8–10% | 6–8% |

### Return Metrics

```
Cash-on-Cash Return = Annual Pre-Tax Cash Flow / Total Equity Invested

Equity Multiple = Total Cash Distributions / Total Equity Invested
  (also called MOIC — Multiple on Invested Capital)

Unlevered IRR = IRR of cash flows: {−Purchase Price, NOI₁−CapEx₁, ..., NOIₙ−CapExₙ+Reversion}
Levered IRR   = IRR of equity cash flows: {−Equity, LCFAT₁, ..., LCFATₙ+Net Reversion}
```

**IRR computation** — always use numpy/scipy:

```python
import numpy as np

# Example: 5-year hold
cash_flows = [-equity_invested, lcf_yr1, lcf_yr2, lcf_yr3, lcf_yr4, lcf_yr5 + net_reversion]
levered_irr = np.irr(cash_flows)  # or numpy_financial.irr()

# Equity multiple
equity_multiple = sum(cash_flows[1:]) / abs(cash_flows[0])
```

### Disposition / Reversion

```
Gross Sale Price      = Forward NOI / Exit Cap Rate
(−) Disposition Costs = Gross Sale Price × Cost Rate (typically 1.5–3.0%)
= Net Sale Proceeds
(−) Loan Payoff       = Outstanding Balance + Prepayment Penalty (if any)
= Net Equity Proceeds
```

---

## 2. Lease Rollover Modeling

When tenants' leases expire, model re-leasing with these assumptions:

```
Renewal Probability: 60–75% (existing tenants)
New Tenant Downtime:  3–12 months (varies by market/asset type)
Tenant Improvements:
  - Renewal: $5–$20/SF (varies by asset type)
  - New Tenant: $20–$60/SF (varies by asset type)
Leasing Commissions:
  - New: 4–6% of aggregate lease value
  - Renewal: 2–3% of aggregate lease value
```

**Mark-to-market adjustment:**
```
If In-Place Rent < Market Rent → positive mark-to-market (upside)
If In-Place Rent > Market Rent → negative mark-to-market (risk)
Mark-to-Market (%) = (Market Rent − In-Place Rent) / In-Place Rent
```

---

## 3. Capital Stack Structuring

### Standard Capital Stack (Acquisition)

```
Total Capitalization = Purchase Price + Closing Costs + Reserves + Day-1 CapEx

Components:
1. Senior Debt         (typically 55–70% of value)
2. Mezzanine Debt      (optional, 10–15%)
3. Preferred Equity    (optional, 5–15%)
4. Common Equity       (remainder)
   a. GP Equity        (typically 5–20% of total equity)
   b. LP Equity        (remainder)
```

### Closing Cost Estimate

| Item | Typical Range |
|------|--------------|
| Title & Escrow | 0.1–0.3% of price |
| Legal | $50K–$250K |
| Due Diligence (inspections, environmental, surveys) | $25K–$100K |
| Lender Fees (origination, appraisal, legal) | 0.5–1.5% of loan |
| Transfer Tax | Varies by jurisdiction |
| Broker Commission (if applicable) | 0.5–1.0% of price |
| **Total Closing Costs** | **1.5–3.5% of price** |

---

## 4. Sensitivity Analysis Methodology

### Two-Variable Sensitivity

The standard underwriting sensitivity matrix varies two key assumptions simultaneously:

**Primary matrix**: Exit Cap Rate vs. Rent Growth Rate → Levered IRR
**Secondary matrix**: LTV vs. Interest Rate → DSCR and Levered IRR

### Construction rules:
1. Base case sits at the center of the matrix
2. Vary each axis in equal increments (e.g., 25bps for cap rates, 50bps for rent growth)
3. Include at least 5 rows and 5 columns (25 scenarios minimum)
4. Color-code results: green = meets hurdle, yellow = marginal, red = below hurdle
5. Highlight the base case cell

### Scenario Analysis

Define four standard scenarios:

| Scenario | Vacancy Adj | Rent Growth Adj | Exit Cap Adj | CapEx Adj | Probability |
|----------|-------------|-----------------|--------------|-----------|-------------|
| **Bull** | −200bps | +100bps | −25bps | −10% | 15–20% |
| **Base** | As modeled | As modeled | As modeled | As modeled | 45–55% |
| **Bear** | +300bps | −100bps | +50bps | +15% | 20–25% |
| **Stress** | +500bps | −200bps | +100bps | +25% | 5–10% |

```
Probability-Weighted IRR = Σ (Scenario IRR × Probability Weight)
Probability-Weighted EM  = Σ (Scenario EM × Probability Weight)
```

---

## 5. Risk Scoring Framework

### Risk Categories

Score each factor on two dimensions:

- **Severity** (1–5): Impact on returns if the risk materializes
- **Likelihood** (1–5): Probability the risk materializes during hold period

```
Risk Score = Severity × Likelihood

Risk Classification:
  1–6   = LOW (monitor)
  7–14  = MODERATE (mitigate)
  15–25 = CRITICAL (must address before proceeding)
```

### Standard Risk Factors

| # | Risk Factor | What to Assess |
|---|-------------|----------------|
| 1 | **Tenant Concentration** | Top tenant as % of rent; top 3 tenants as % of rent |
| 2 | **Lease Rollover** | % of rent expiring within 24 months; WALT |
| 3 | **Market / Submarket** | Supply pipeline, absorption trends, rent trajectory |
| 4 | **Interest Rate / Refi** | Rate sensitivity, loan maturity vs. hold period |
| 5 | **CapEx Overrun** | Scope uncertainty, contractor risk, permits |
| 6 | **Environmental** | Phase I findings, flood zone, seismic, contamination |
| 7 | **Regulatory** | Rent control, zoning changes, tax reassessment |
| 8 | **Execution** | Value-add plan complexity, sponsor track record |

---

## 6. Return Hurdles by Strategy

Use these benchmarks to evaluate whether a deal meets minimum return thresholds:

| Strategy | Target Levered IRR | Target Equity Multiple | Target Cash-on-Cash (Stabilized) | Typical Hold |
|----------|-------------------|----------------------|----------------------------------|--------------|
| Core | 6–9% | 1.3–1.6x | 4–6% | 7–10 years |
| Core-Plus | 9–13% | 1.4–1.8x | 5–7% | 5–7 years |
| Value-Add | 13–18% | 1.6–2.2x | 6–9% | 3–5 years |
| Opportunistic | 18%+ | 2.0x+ | Varies | 2–5 years |

**Decision framework:**
```
IF Probability-Weighted IRR >= Strategy Hurdle
   AND DSCR >= 1.25x (all years)
   AND No CRITICAL risks unmitigated
   → PROCEED

IF Probability-Weighted IRR >= Strategy Hurdle
   BUT (DSCR < 1.25x in any year OR CRITICAL risks present)
   → PROCEED WITH CONDITIONS (list conditions)

IF Probability-Weighted IRR < Strategy Hurdle
   → PASS (state shortfall)
```

---

## 7. Presentation Standards

### Formatting Rules

- All dollar amounts: comma-separated, no decimals for amounts > $1,000 (e.g., $1,250,000)
- Per-SF amounts: two decimals (e.g., $28.50/SF)
- Percentages: one decimal for rates (e.g., 6.5%), two decimals for IRR (e.g., 14.23%)
- Cap rates: two decimals in basis points context (e.g., 5.75%), or "575 bps"
- Multiples: one decimal with "x" suffix (e.g., 1.8x)
- Always label: gross vs. net, annual vs. monthly, levered vs. unlevered

### Required Provenance Tags

Every key metric must carry one of:

| Tag | Meaning |
|-----|---------|
| **VERIFIED** | Cross-referenced against multiple independent sources |
| **REPORTED** | Taken directly from a single source document |
| **ESTIMATED** | Derived from comparable data or market benchmarks |
| **ASSUMED** | Analyst assumption with stated rationale |

---

## 8. Common Pitfalls

1. **Mixing trailing and forward NOI** — Going-in cap uses trailing; exit cap uses forward. Mixing them makes returns unreliable.
2. **Ignoring lease-up costs during vacancy** — TI, LC, and downtime reduce effective returns materially. Always model them.
3. **Straight-lining expenses** — Taxes can spike on reassessment; insurance can jump; maintenance is lumpy. Use realistic escalation curves.
4. **Omitting prepayment penalties** — Yield maintenance or defeasance costs at disposition can reduce returns by 100–300bps.
5. **Understating closing costs** — A common error is modeling 1% when actual costs are 2–3.5%.
6. **Double-counting reserves** — Reserves for replacement are an OpEx line item. Don't also deduct them as CapEx.
7. **Ignoring tax reassessment** — Many jurisdictions reassess on sale. Model post-acquisition taxes, not seller's taxes.
8. **Using nominal cap rate spreads** — Always compare going-in cap rate to risk-free rate (10-year Treasury) for relative value context.
