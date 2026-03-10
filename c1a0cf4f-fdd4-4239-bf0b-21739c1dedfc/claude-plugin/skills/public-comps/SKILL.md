---
description: >
  Public market comparable company analysis for PE portfolio valuation. Triggers on:
  "public comps", "comparable companies", "trading multiples", "stock performance",
  "public market", "comp set", "valuation comps", "market comparables", "key comps",
  "public comp impact". Provides methodology for identifying, analyzing, and applying
  public company comparables to private portfolio company valuations.
---

# Public Comps — Public Market Comparable Analysis

## Purpose

Identify and analyze public market comparables for PE portfolio companies. Map trading multiples, stock performance, and sector trends to inform private company valuations and portfolio monitoring.

## Comp Selection Criteria

Select 3-5 public comparables per portfolio company based on:

1. **Business model similarity** (weight: 30%) — same value chain position, revenue model
2. **End market overlap** (weight: 25%) — same customers, industry vertical
3. **Revenue scale proximity** (weight: 20%) — within 0.5x-3.0x revenue range preferred
4. **Growth profile similarity** (weight: 15%) — similar growth rate trajectory
5. **Geographic overlap** (weight: 10%) — same primary operating geographies

## Data Points to Capture

### Per Comp

| Data Point | Format | Source Requirement |
|-----------|--------|-------------------|
| Market Cap | $XM/$XB | Provider + date |
| Enterprise Value | $XM/$XB | Provider + date |
| LTM Revenue | $XM | Filing or consensus |
| NTM Revenue (est.) | $XM | Consensus + source |
| LTM EBITDA | $XM | Filing or consensus |
| NTM EBITDA (est.) | $XM | Consensus + source |
| Revenue Growth (YoY) | X.X% | Filing |
| EBITDA Margin | X.X% | Filing |
| EV/Revenue (LTM) | X.Xx | Calculated |
| EV/Revenue (NTM) | X.Xx | Calculated |
| EV/EBITDA (LTM) | X.Xx | Calculated |
| EV/EBITDA (NTM) | X.Xx | Calculated |
| P/E Ratio | X.Xx | Provider |
| YTD Stock Return | X.X% | Provider + date |
| 1Y Stock Return | X.X% | Provider + date |
| 52W High/Low | $X/$X | Provider |
| Beta | X.XX | Provider |

### Per Comp Set (Aggregates)

Calculate: Mean, Median, High, Low, 25th percentile, 75th percentile for all multiple metrics.

## Portco Valuation Impact

For each portfolio company, show how comp movements affect marks:

**Implied Valuation** = Portco Metric × Comp Set Median Multiple

| Approach | Formula | Example |
|----------|---------|---------|
| EV/EBITDA | Portco EBITDA × Comp Median EV/EBITDA | $50M × 12.0x = $600M EV |
| EV/Revenue | Portco Revenue × Comp Median EV/Revenue | $200M × 4.0x = $800M EV |

**Premium/Discount Analysis:**
- Compare portco's current mark multiple to comp median
- Express as premium/(discount): "+15% premium" or "(20%) discount"
- Justify premium/discount with specific factors (growth, profitability, size, liquidity)

## Sector Read-Through

For each comp set, synthesize:
1. **Earnings themes**: Common guidance revisions, margin commentary, demand trends
2. **Sector tailwinds/headwinds**: Macro, regulatory, competitive dynamics
3. **M&A activity**: Recent transactions, strategic premiums observed
4. **Analyst consensus shifts**: Upgrades/downgrades, target price movements

Always attribute to specific analyst reports with dates.

## Source Attribution Requirements

- All market data: cite provider (Bloomberg, Capital IQ, Yahoo Finance, FactSet) + as-of date
- Consensus estimates: cite source (Bloomberg consensus, FactSet consensus) + date
- Analyst commentary: cite "[Bank] [Analyst Name if available], [Date]"
- Trading data is intraday: specify time if same-day

## Critical Rules

1. **LTM vs. NTM**: Always state clearly which basis is used for multiples
2. **EV vs. Equity**: Never mix enterprise value and equity value multiples
3. **Liquidity discount**: Note that private company marks should generally reflect a liquidity/size discount to public comps (typically 10-30%)
4. **Pending M&A**: Flag any comps with announced or rumored M&A — their multiples reflect acquisition premium
5. **Outliers**: If a comp is >2 standard deviations from the set median, note it and consider excluding from aggregates
6. **Staleness**: Market data should be no more than 5 business days old for active monitoring
