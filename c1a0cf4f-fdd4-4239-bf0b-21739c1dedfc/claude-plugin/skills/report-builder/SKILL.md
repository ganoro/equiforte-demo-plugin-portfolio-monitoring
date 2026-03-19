---
name: report-builder
description: Assemble a complete daily market brief report in markdown from market data, geopolitical developments, and event calendar data. Use when all daily brief data has been collected and needs to be formatted into the final deliverable.
---

# Daily Brief Report Builder

Assemble the final daily market brief from data collected by the market-snapshot, geopolitical-monitor, and event-calendar skills. The output is a single markdown file that is fact-dense, scannable, and free of opinion.

## Report Structure

The report must follow this exact structure. Do not omit sections. If a section has no data, state "No significant developments."

```markdown
# Daily Market Brief — [Day, Month DD, YYYY]

> Generated at [HH:MM ET]. Data as of prior close unless noted.
> Focus: [All / PE / PD / HF / IB]

---

## 1. Market Snapshot

### US Equities
| Index | Close | Change | % Change | YTD |
|---|---|---|---|---|

### European Equities
| Index | Close | Change | % Change | YTD |
|---|---|---|---|---|

### Asia-Pacific Equities
| Index | Close | Change | % Change | YTD |
|---|---|---|---|---|

### US Sector Performance
| Sector | Close | % Change | YTD |
|---|---|---|---|
[Sorted by daily % change, best to worst]

### US Treasuries & Rates
| Maturity | Yield | Change (bps) | WTD | MTD |
|---|---|---|---|---|

Curve: 2s10s spread [X] bps ([+/-X] bps)

### Global Sovereign Yields (10Y)
| Country | Yield | Change (bps) |
|---|---|---|

### Credit Spreads
| Measure | Level | Change (bps) | MTD |
|---|---|---|---|

### Commodities
| Commodity | Price | Change | % Change | YTD |
|---|---|---|---|---|

### Foreign Exchange
| Pair | Rate | Change | % Change |
|---|---|---|---|

DXY: [level] ([+/-X]%)

### Volatility & Sentiment
| Indicator | Level | Change |
|---|---|---|

---

## 2. Economic Data Releases

### Today's Releases
| Time (ET) | Country | Indicator | Period | Actual | Prior | Consensus | Surprise |
|---|---|---|---|---|---|---|---|

[For each notable release, add a single factual line: "[Indicator] came in at [X] vs consensus [Y], [above/below/in line]. Prior was revised [up/down] to [Z] from [W]." — no interpretation of what this means for policy or markets.]

---

## 3. Central Bank & Policy

[Items from geopolitical-monitor Step 1, formatted as:]

**[Speaker/Event]** ([Time ET])
[Factual summary. Direct quotes for key policy language.]

---

## 4. Geopolitical & Macro Developments

[Items from geopolitical-monitor Steps 3-6, formatted as:]

**[Headline]**
[1-3 sentence factual description.] Source: [source].

---

## 5. Corporate & Deal Activity

### Major Transactions
| Date | Type | Parties | Value | Status |
|---|---|---|---|---|

### Notable Corporate Events
- [Event descriptions]

---

## 6. Upcoming Calendar

### Rest of This Week
[Day-by-day list from event-calendar]

### Next Week Highlights
[Key events only, grouped by category]

### Key Earnings This Week
| Date | Time | Company | Ticker | EPS Est | Rev Est |
|---|---|---|---|---|---|

### Conferences & Events (Next 4 Weeks)
| Dates | Event | Location | Key Sectors |
|---|---|---|---|

### Auction & Issuance Calendar
[Treasury auctions, notable corporate issuance]

---

## 7. Focus Section: [PE / PD / HF / IB]

[Include ONLY if a specific focus was requested. This section surfaces data from the above sections that is particularly relevant to the focus area, plus additional focus-specific data.]

### For PE Focus:
- Sponsor-backed M&A announced/closed (from deal activity)
- Leveraged loan / HY market conditions (from credit spreads)
- Notable PE fund closings or fundraises
- PE-relevant conferences upcoming
- Portfolio company earnings this week
- EBITDA purchase multiple trends (if data available)

### For PD / Credit Focus:
- Leveraged loan index levels and flows
- CLO new issuance and spread trends
- Default rate updates (S&P/Moody's trailing 12-month)
- Distressed names / watchlist additions
- Direct lending benchmark rates
- Credit-focused conference calendar

### For HF Focus:
- Sector factor performance (value, growth, momentum, quality)
- Short interest changes (most shorted names)
- ETF flows (equity, fixed income, commodity)
- Options market activity (put/call ratio, notable large trades)
- Cross-asset correlation snapshot
- CTA/systematic positioning indicators (if available)

### For IB Focus:
- ECM activity (IPOs priced, filed, withdrawn)
- DCM activity (IG/HY issuance volumes, notable deals)
- M&A league table activity
- Advisory mandates announced
- Sector deal volume trends

---

## Sources & Disclaimers

Data sourced from: [list MCP servers and web sources used].
All data as of [timestamp]. Markets may have moved since publication.
This briefing contains facts and data only. No investment recommendations or opinions are expressed.
```

## Formatting Rules

1. **Tables**: Use proper markdown tables. Align numbers right-justified where possible. Use consistent decimal places (2 for prices, 1 for yields, 2 for FX rates).

2. **Directional indicators**:
   - Positive changes: `+1.23` or `+0.45%`
   - Negative changes: `-1.23` or `-0.45%`
   - Unchanged: `0.00` or `UNCH`

3. **Abbreviations** (use consistently):
   - bps = basis points
   - BMO = before market open
   - AMC = after market close
   - WTD = week-to-date
   - MTD = month-to-date
   - YTD = year-to-date
   - EST/ACT = estimate/actual
   - N/A = not available

4. **Numbers**:
   - Billions: `$12.3B`
   - Millions: `$456.7M`
   - Thousands: `$89.1K`
   - Percentages: `3.45%`
   - Basis points: `+5 bps`

5. **No interpretation rule**: The report may state directional facts ("the S&P 500 fell 1.2%", "CPI came in above consensus") but must NEVER:
   - Speculate on causes ("fell due to tariff fears")
   - Predict outcomes ("this suggests the Fed will...")
   - Characterize magnitude subjectively ("plunged", "soared", "surprisingly strong")
   - Recommend actions ("investors should consider...")
   - Use words like: bullish, bearish, hawkish, dovish, risk-on, risk-off, rally, selloff, rout, surge

   Acceptable: "fell", "rose", "declined", "gained", "was unchanged", "above consensus", "below prior"

6. **Data freshness**: Always include the timestamp of data collection. If a data point is stale (>24h), note this.

7. **Length target**: The full report should be 800-1500 lines of markdown depending on how much is happening. A quiet day should still have all sections populated with available data.

## Quality Checklist

Before finalizing the report:

- [ ] Every number has a source
- [ ] All tables are properly formatted and render in markdown
- [ ] No interpretive or subjective language anywhere in the report
- [ ] All sections present (even if "No significant developments")
- [ ] Timestamps are consistent and accurate
- [ ] Focus section included if requested, omitted if not
- [ ] File written to the specified output path
- [ ] Directional indicators (+/-) present on all changes
- [ ] No data is fabricated — `N/A` used for unavailable data
