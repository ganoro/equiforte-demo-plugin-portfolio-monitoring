---
name: report-builder
description: Assemble a complete daily market brief report in markdown from market data, geopolitical developments, and event calendar data. Use when all daily brief data has been collected and needs to be formatted into the final deliverable.
---

# Daily Brief Report Builder

Assemble the final daily market brief from collected data. Output a single markdown file that is fact-dense, scannable, and free of opinion.

## CRITICAL: Efficiency Rules

- **DO NOT** make any additional web searches or data lookups. Use only the data already collected.
- **DO NOT** add sections or data beyond what was gathered. If a data point was not collected, omit it or mark `N/A`.
- **DO** write the report in a single pass. No drafts, no revisions.
- **Target length: 300-600 lines.** Do not pad with empty rows or verbose descriptions.

## Report Template

Write the report following this structure exactly. Populate tables directly from collected data.

```markdown
# Daily Market Brief — [Day, Month DD, YYYY]

> Data as of prior close unless noted. Focus: [All / PE / PD / HF / IB]

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

### US Treasuries & Rates
| Maturity | Yield | Change (bps) |
|---|---|---|

2s10s spread: [X] bps ([+/-X])

### Global 10Y Yields
| Country | Yield | Change (bps) |
|---|---|---|

### Credit Spreads
| Measure | Level | Change (bps) |
|---|---|---|

### Commodities
| Commodity | Price | Change | % Change |
|---|---|---|---|

### FX
| Pair | Rate | Change | % Change |
|---|---|---|---|

DXY: [level] ([+/-X]%)

### Volatility
| Indicator | Level | Change |
|---|---|---|

---

## 2. Economic Data Releases

| Time (ET) | Country | Indicator | Actual | Prior | Consensus | Surprise |
|---|---|---|---|---|---|---|

---

## 3. Central Bank & Policy

[Only items from today. Each as:]
**[Speaker/Event]** — [Factual summary with direct quotes for key language.]

---

## 4. Geopolitical & Macro Developments

[Each as:]
**[Headline]** — [1-2 sentences.] Source: [source].

---

## 5. Corporate & Deal Activity

| Type | Parties | Value | Status |
|---|---|---|---|

---

## 6. Upcoming Calendar

### This Week (remaining)
[Day-by-day: economic releases, earnings, events on each day]

### Next Week Highlights
[Key events grouped by category]

### Key Earnings
| Date | Time | Company | Ticker | EPS Est | Rev Est |
|---|---|---|---|---|---|

### Conferences (Next 4 Weeks)
| Dates | Event | Location | Sectors |
|---|---|---|---|

---

## 7. Focus Section: [PE / PD / HF / IB]

[ONLY if focus was requested. Pull relevant items from above sections — do not add new data.]

---

Sources: [list sources used]. This briefing contains facts and data only.
```

## Formatting Rules

- Positive: `+1.23` / `+0.45%`. Negative: `-1.23` / `-0.45%`. Unchanged: `UNCH`
- Billions: `$12.3B`, Millions: `$456.7M`, bps: `+5 bps`
- **No interpretation**: state direction ("fell", "rose", "above consensus") but never speculate on causes, predict outcomes, or use subjective words (bullish, bearish, hawkish, dovish, surge, plunge, soar, rout, rally, selloff, risk-on, risk-off)

## Quality Checklist

- [ ] All tables render in markdown
- [ ] No interpretive language
- [ ] All sections present (even if "No significant developments")
- [ ] `N/A` for missing data, never fabricated
- [ ] Report written to output path
