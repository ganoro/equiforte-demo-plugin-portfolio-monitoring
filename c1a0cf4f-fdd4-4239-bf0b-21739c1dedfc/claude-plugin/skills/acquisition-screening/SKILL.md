---
description: >
  M&A target screening and evaluation framework for PE portfolio add-ons and new platforms.
  Triggers on: "acquisition targets", "add-on", "bolt-on", "M&A screening", "deal sourcing",
  "target identification", "acquisition pipeline", "buy-and-build", "platform investment",
  "investment targets". Provides methodology for screening, scoring, and evaluating potential
  acquisition targets.
---

# Acquisition Screening — M&A Target Identification

## Purpose

Screen, score, and evaluate potential acquisition targets for PE portfolios — either add-on acquisitions for existing platform companies or new platform investments.

## Screening Framework

### Step 1 — Define Criteria

Establish screening parameters from user input and fund mandate:

| Criterion | Source | Default if not specified |
|-----------|--------|------------------------|
| Revenue range | User/fund mandate | $10M-$500M |
| EBITDA margin | Sector benchmark | >10% |
| Growth rate | User/fund mandate | >5% YoY |
| Geography | User/fund mandate | North America |
| Sector/sub-sector | User/portco context | Match existing portco |
| Max entry multiple | Back-solve from min IRR | Fund historical range |
| Revenue quality | User preference | >40% recurring |
| Customer concentration | Risk threshold | <25% top customer |

### Step 2 — Back-Solve Entry Multiple from IRR Target

If user specifies a minimum IRR expectation:

**Max Entry Multiple** = f(Target IRR, Hold Period, Exit Multiple, Revenue Growth, Margin Expansion)

Show the sensitivity:

| Entry EV/EBITDA | 5Y Exit at 8x | 5Y Exit at 10x | 5Y Exit at 12x |
|-----------------|---------------|----------------|----------------|
| 6.0x | XX% IRR | XX% IRR | XX% IRR |
| 8.0x | XX% IRR | XX% IRR | XX% IRR |
| 10.0x | XX% IRR | XX% IRR | XX% IRR |

### Step 3 — Strategic Fit Scoring

For each candidate, score on:

| Dimension | Weight | Scale | What to assess |
|-----------|--------|-------|----------------|
| Revenue synergy | 20% | 1-5 | Cross-sell potential, market access, pricing power |
| Cost synergy | 15% | 1-5 | Procurement, shared services, facility consolidation |
| Geographic fit | 15% | 1-5 | New markets vs. overlap, expansion potential |
| Capability add | 20% | 1-5 | Technology, talent, IP, product/service gaps filled |
| Cultural fit | 15% | 1-5 | Management style, company stage, organizational structure |
| Customer overlap | 15% | 1-5 | Complementary vs. competing customer base |

**Fit Score** = Weighted average (max 5.0)

### Step 4 — Preliminary Returns Analysis

For top candidates (Fit Score ≥ 3.5), build illustrative returns:

- Entry valuation range (based on sector multiples and screening criteria)
- 5-year projected EBITDA (using estimated growth + synergies)
- Exit multiple range (comp-based)
- Gross MOIC and Gross IRR at base case
- Highlight which targets meet minimum IRR expectations

### Step 5 — Risk Flagging

For each candidate, flag:
- Customer concentration risk
- Key person dependency
- Regulatory/compliance complexity
- Integration risk (technology, culture, operations)
- Competitive position vulnerability
- Data quality (how reliable are the estimates?)

## Client Customization

- All screening criteria are adjustable — user can add, remove, or change thresholds
- Scoring weights are adjustable — user can emphasize strategic fit vs. financial returns
- Min IRR can be set to filter out targets that don't meet return threshold
- Geography, sector, and size can be narrowed or expanded at any time

## Data Sources

Use public information only:
- Company websites and press releases
- Industry reports and databases (PitchBook, Crunchbase)
- Conference presentations and trade publications
- Regulatory filings (if public)
- News articles and M&A announcements

Always cite source. Never present estimates as facts.

## Critical Rules

1. All financial figures for private targets are ESTIMATED — label clearly
2. This is screening, not due diligence — note preliminary nature
3. Don't present as investment recommendation — present as analysis for consideration
4. Flag known deal processes, advisors, or competitive dynamics
5. Distinguish between "actionable" (likely available) vs. "aspirational" (may not be for sale)
6. Max 8-12 candidates per screen — quality over quantity
