---
name: market-snapshot
description: Collect current global market data across equity indices, fixed income, commodities, currencies, and volatility. Use when generating a daily brief or when the user asks for a market snapshot, market overview, or current market levels.
---

# Market Snapshot

Collect fact-based market data for the daily brief. Every number must be sourced.

## CRITICAL: Search Efficiency Rules

You have a **budget of 8 web searches maximum** for this entire skill. Structure searches to maximize data per query.

- **DO NOT** search for individual assets one at a time
- **DO NOT** re-search for "exact" values if a search already returned data — use what you got
- **DO** use broad searches that return dashboard/summary pages with multiple data points
- **DO** accept rounded values from summary pages rather than re-searching for precision
- If a data point is not found in 1 search, mark it `N/A` — do not retry

### Recommended Search Strategy (8 searches)

1. **Search 1 — US & Global Equities**: "major stock market indices closing prices today [date]" → should return S&P 500, DJIA, Nasdaq, Russell 2000, FTSE, DAX, CAC, Nikkei, Hang Seng, Shanghai in one page
2. **Search 2 — US Treasury Yields & Rates**: "US treasury yields today 2-year 10-year 30-year [date]" → yields, spreads, Fed Funds, SOFR
3. **Search 3 — Credit Spreads**: "investment grade high yield credit spreads CDX leveraged loan index today" → IG/HY OAS, CDX, LSTA
4. **Search 4 — Commodities**: "commodity prices today oil gold copper natural gas [date]" → WTI, Brent, gold, silver, copper, natgas
5. **Search 5 — FX & DXY**: "US dollar index major currency pairs today EUR USD JPY GBP [date]" → DXY, all major pairs
6. **Search 6 — Volatility**: "VIX MOVE index put call ratio today [date]" → VIX, MOVE, P/C ratio
7. **Search 7 — EM currencies & crypto**: "emerging market currencies bitcoin ethereum price today [date]"
8. **Search 8 — Global sovereign yields**: "global 10 year bond yields Germany UK Japan today [date]"

## Data to Collect

### Global Equity Indices

**Core (must have)**
- S&P 500, DJIA, Nasdaq Composite, Russell 2000
- FTSE 100, Euro Stoxx 50, DAX, CAC 40
- Nikkei 225, Hang Seng, Shanghai Composite
- Sensex/Nifty 50

**If available from same search (do not search separately)**
- S&P/TSX, Bovespa, KOSPI, ASX 200, SMI, IBEX, FTSEMIB, STI, CSI 300

**US Sector Performance** — only include if returned by a search; do not search separately.

### Fixed Income & Rates

**Core**: US 2Y, 5Y, 10Y, 30Y yields + 2s10s spread
**Global 10Y**: German Bund, UK Gilt, Japan JGB (others if available)
**Credit**: IG OAS, HY OAS, CDX.NA.IG, CDX.NA.HY, S&P/LSTA Leveraged Loan Index
**Money markets**: Fed Funds, SOFR, ECB rate, BoE rate (do not search separately — include if found)

### Commodities

**Core**: WTI, Brent, Natural Gas, Gold, Silver, Copper
**If available**: Iron Ore, Wheat, Corn, Soybeans

### Foreign Exchange

**Core**: DXY, EUR/USD, GBP/USD, USD/JPY, USD/CHF, AUD/USD, USD/CAD
**EM**: USD/CNY, USD/BRL, USD/MXN (others if available)
**Crypto**: BTC/USD, ETH/USD

### Volatility

**Core**: VIX, MOVE Index
**If available**: Put/Call Ratio, VVIX

## Output Format

For each asset class, report in a table:

```
| Asset | Last | Change | % Change | YTD |
```

- Positive changes: `+`, Negative: `-`
- Rate changes in bps
- `N/A` for unavailable data — never estimate
- Report daily change only. WTD/MTD/YTD only if returned by search — do not compute or search separately.

## Data Sources

Use MCP servers (Morningstar, LSEG, FactSet, S&P Global) as primary. Supplement with web search for gaps.
