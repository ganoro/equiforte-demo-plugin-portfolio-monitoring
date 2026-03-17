---
name: underwriting
description: Perform a full underwriting analysis on a real estate or PE/VC deal — proforma construction, return modeling, risk assessment, sensitivity analysis, and investment recommendation
tags:
  - underwriting
  - real-estate
  - cre
  - pe
  - vc
  - deal-analysis
  - proforma
  - irr
  - returns
  - investment
  - acquisition
  - due-diligence
placeholder: "e.g. Underwrite the acquisition of 500 Commerce Drive, a 120,000 SF Class A office building at $28M"
defaultOutput: Spreadsheet
icon: IconFileAnalytics
arguments:
  - name: deal
    description: "Property/company name, address, deal description, or 'analyze' to run on workspace data"
    required: false
  - name: strategy
    description: "Investment strategy: core, core-plus, value-add, opportunistic (default: infer from deal)"
    required: false
  - name: hold-period
    description: "Projected hold period in years (default: 5)"
    required: false
---

# /underwriting — Deal Underwriting Analysis

Perform a comprehensive underwriting analysis for a real estate acquisition or PE/VC investment. Produces a full proforma, return waterfall, risk assessment, and go/no-go recommendation backed by quantitative evidence.

## Target

**$ARGUMENTS** (default: analyze workspace data for deal context)

## Instructions

### Step 1 — Gather & Validate Deal Inputs

Scan the workspace for all deal-related documents: offering memoranda (OM), rent rolls, financials, appraisals, environmental reports, loan docs, and market comps. Use the `document-parser` skill for PDF/XLSX extraction.

Extract and organize these **core deal parameters**:

| Parameter | Value | Source | Confidence |
|-----------|-------|--------|------------|
| Property/Asset Name | | | |
| Location (City, State, Submarket) | | | |
| Asset Type (Office, Multifamily, Industrial, Retail, Mixed-Use) | | | |
| Year Built / Renovated | | | |
| Gross Leasable Area (SF) or Unit Count | | | |
| Asking Price / Offer Price | | | |
| Current Occupancy (%) | | | |
| In-Place NOI (trailing 12-month) | | | |
| Going-In Cap Rate (Price / T-12 NOI) | | | |
| Investment Strategy (Core / Core-Plus / Value-Add / Opportunistic) | | | |
| Target Hold Period (years) | | | |

If any critical parameter is missing, flag it as a **data gap** and state what assumption was used. Never fabricate inputs — record provenance for every figure.

### Step 2 — Build the Revenue Proforma

Construct a year-by-year revenue projection for the full hold period plus a disposition year.

**2a. In-Place Revenue Schedule**

Build from the rent roll (use the `/rent-roll` command output if available):

| Year | Occupied SF | Vacancy (%) | Effective Rent/SF | Gross Potential Rent | Vacancy & Credit Loss | Effective Gross Revenue |
|------|-------------|-------------|-------------------|---------------------|-----------------------|------------------------|

**2b. Lease Rollover & Re-Leasing Assumptions**

For each year, model lease expirations and re-leasing:

| Year | Expiring SF | Renewal Probability (%) | Market Rent/SF | Downtime (months) | TI/SF | LC/SF | Net Re-Leasing Revenue Impact |
|------|-------------|------------------------|----------------|-------------------|-------|-------|-------------------------------|

**2c. Other Income**

Include all ancillary income streams (parking, storage, antenna, laundry, percentage rent, etc.):

| Income Source | Year 1 | Annual Growth (%) | Basis |
|---------------|--------|-------------------|-------|

**2d. Total Revenue Summary**

| Year | 1 | 2 | 3 | 4 | 5 | Disposition Year |
|------|---|---|---|---|---|-----------------|
| Gross Potential Rent | | | | | | |
| (−) Vacancy & Credit Loss | | | | | | |
| (+) Other Income | | | | | | |
| **= Effective Gross Income (EGI)** | | | | | | |

### Step 3 — Model Operating Expenses & Capital Expenditures

**3a. Operating Expense Budget**

| Expense Category | Year 1 ($) | $/SF | % of EGI | Annual Escalation (%) |
|-----------------|------------|------|----------|----------------------|
| Real Estate Taxes | | | | |
| Insurance | | | | |
| Utilities | | | | |
| Repairs & Maintenance | | | | |
| Property Management (% of EGI) | | | | |
| General & Administrative | | | | |
| Janitorial / Landscaping | | | | |
| Marketing / Leasing | | | | |
| Reserves for Replacement | | | | |
| **Total Operating Expenses** | | | | |

**3b. Capital Expenditure Schedule**

| CapEx Item | Timing (Year) | Amount ($) | $/SF | Funding Source |
|------------|---------------|------------|------|---------------|
| Deferred Maintenance | | | | |
| Tenant Improvements (new) | | | | |
| Tenant Improvements (renewals) | | | | |
| Leasing Commissions | | | | |
| Value-Add Renovation | | | | |
| **Total CapEx** | | | | |

**3c. Net Operating Income (NOI) Proforma**

| Year | 1 | 2 | 3 | 4 | 5 | Disposition Year |
|------|---|---|---|---|---|-----------------|
| EGI | | | | | | |
| (−) Operating Expenses | | | | | | |
| **= NOI** | | | | | | |
| NOI Growth (%) | — | | | | | |
| NOI Margin (%) | | | | | | |

### Step 4 — Structure the Capital Stack & Debt Service

Model the acquisition financing and annual debt service:

| Capital Stack Component | Amount ($) | % of Total | Rate / Return | Term |
|------------------------|------------|------------|---------------|------|
| Senior Debt | | | | |
| Mezzanine / Preferred Equity | | | | |
| GP Equity | | | | |
| LP Equity | | | | |
| **Total Capitalization** | | | | |

**Debt Service Schedule:**

| Year | Beginning Balance | Interest | Amortization | Total Debt Service | Ending Balance | DSCR |
|------|-------------------|----------|--------------|-------------------|----------------|------|
| 1 | | | | | | |
| 2 | | | | | | |
| 3 | | | | | | |
| 4 | | | | | | |
| 5 | | | | | | |

Loan-to-Value (LTV): ___% | Debt Yield: ___% | Interest Coverage Ratio: ___x

### Step 5 — Compute Return Metrics & Waterfall

Use the `underwriting` skill for all formulas and methodology. Use the `financial-modeler` agent for computation.

**5a. Unlevered Cash Flow & Returns**

| Year | NOI | (−) CapEx | = Unlevered FCF | Reversion (Disposition Year) |
|------|-----|-----------|-----------------|------------------------------|

- **Unlevered IRR**: ___%
- **Equity Multiple (Unlevered)**: ___x

**5b. Levered Cash Flow & Returns**

| Year | NOI | (−) Debt Service | (−) CapEx | = Levered FCF | Reversion Net of Loan Payoff |
|------|-----|-------------------|-----------|---------------|------------------------------|

- **Levered IRR**: ___%
- **Equity Multiple (Levered)**: ___x
- **Cash-on-Cash Return (Year 1)**: ___%
- **Average Cash-on-Cash (Hold Period)**: ___%

**5c. Disposition Assumptions**

| Metric | Value | Basis |
|--------|-------|-------|
| Exit Cap Rate | | |
| Exit Cap Rate Spread vs. Entry | | |
| Disposition NOI (forward) | | |
| Gross Sale Price | | |
| (−) Disposition Costs (%) | | |
| = Net Sale Proceeds | | |
| (−) Loan Payoff | | |
| = Net Equity Proceeds | | |

**5d. GP/LP Waterfall (if applicable)**

Use the `fund-performance` skill for waterfall computation. Show preferred return, catch-up, and promote tiers.

### Step 6 — Sensitivity & Scenario Analysis

Run the `financial-modeler` agent for quantitative scenario analysis.

**6a. Two-Variable Sensitivity Table — Levered IRR**

Vary exit cap rate (rows) vs. rent growth (columns):

| Exit Cap / Rent Growth | 0% | 1% | 2% | 3% | 4% |
|------------------------|----|----|----|----|-----|
| Entry − 50bps | | | | | |
| Entry Cap | | | | | |
| Entry + 25bps | | | | | |
| Entry + 50bps | | | | | |
| Entry + 100bps | | | | | |

**6b. Scenario Summary**

| Scenario | Description | Levered IRR | Equity Multiple | Probability Weight |
|----------|-------------|-------------|-----------------|-------------------|
| Bull Case | | | | |
| Base Case | | | | |
| Bear Case | | | | |
| Stress Case | | | | |
| **Probability-Weighted** | | | | |

### Step 7 — Risk Assessment & Mitigants

Identify and score the top risks:

| Risk Factor | Severity (1-5) | Likelihood (1-5) | Risk Score | Mitigant |
|-------------|----------------|-------------------|------------|----------|
| Lease Rollover / Tenant Concentration | | | | |
| Market Rent Decline | | | | |
| Interest Rate / Refinancing Risk | | | | |
| CapEx Overrun | | | | |
| Environmental / Regulatory | | | | |
| Submarket Deterioration | | | | |
| Execution Risk (Value-Add Plan) | | | | |

Risk Score = Severity x Likelihood. Flag any risk with score >= 15 as **CRITICAL**.

### Step 8 — Investment Recommendation

Synthesize all analysis into a clear recommendation:

**Summary Dashboard:**

| Metric | Value | Benchmark | Pass/Fail |
|--------|-------|-----------|-----------|
| Going-In Cap Rate | | | |
| Unlevered IRR | | | |
| Levered IRR | | | |
| Equity Multiple | | | |
| Cash-on-Cash (Year 1) | | | |
| DSCR (minimum) | | | |
| Probability-Weighted IRR | | | |
| Risk Score (avg) | | | |

**Recommendation**: PROCEED / PROCEED WITH CONDITIONS / PASS

Provide a 3-5 sentence narrative justification referencing specific metrics, risks, and market context. State the investment strategy (core, core-plus, value-add, opportunistic) and confirm whether the deal meets hurdle rate requirements.

### Step 9 — Write Output

1. Save the full underwriting model as a spreadsheet using the `xlsx-generator` skill
2. Save the narrative summary as a document using the `docx-generator` skill
3. Update entity maps with deal entities, counterparties, and market data points
4. Record all data gaps and assumptions in `_research/gaps.md`

## Critical Rules

- **Every financial figure must state**: as-of date, currency (USD), annual vs. monthly, gross vs. net
- **Cap rates must be mathematically consistent**: Cap Rate = NOI / Value. Verify entry cap, exit cap, and implied cap rates reconcile
- **NOI must reconcile**: EGI − OpEx = NOI. Check every year of the proforma
- **DSCR must be computed correctly**: DSCR = NOI / Total Debt Service. Flag if < 1.25x
- **IRR must be computed from actual cash flows** — never estimated or approximated. Use numpy or scipy for IRR computation
- **Sensitivity tables must be symmetric** around the base case
- **Never fabricate market data** — use provided comps or flag as gaps. All market assumptions must have provenance
- **Disposition value must use forward NOI** (year after exit), not trailing NOI
- **Loan payoff at disposition must include any prepayment penalty** if applicable
- **Expense ratios must be sanity-checked** against asset-type benchmarks (e.g., OpEx typically 35-50% of EGI for office)
- **Label all assumptions explicitly** — distinguish between sponsor assumptions, market data, and analyst estimates
- **Confidence levels required**: Every key metric must carry VERIFIED / REPORTED / ESTIMATED / ASSUMED tag
- **Total capitalization must reconcile**: Senior Debt + Mezz + GP Equity + LP Equity = Purchase Price + Closing Costs + Reserves
- **Equity multiple cross-check**: Equity Multiple = Total Distributions / Total Equity Invested. Must reconcile with IRR
