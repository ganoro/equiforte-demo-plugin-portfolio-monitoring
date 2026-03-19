---
name: market-snapshot
description: Collect current global market data across equity indices, fixed income, commodities, currencies, and volatility. Use when generating a daily brief or when the user asks for a market snapshot, market overview, or current market levels.
---

# Market Snapshot

Collect comprehensive, fact-based market data for the daily brief. Every number must be sourced. Report closing/last values, daily change (absolute and percentage), and week-to-date / month-to-date / year-to-date changes where available.

## Data Collection Workflow

### Step 1: Global Equity Indices

Gather close, daily change, and % change for all of the following:

**Americas**
| Index | Ticker |
|---|---|
| S&P 500 | SPX |
| Dow Jones Industrial Average | DJIA |
| Nasdaq Composite | COMP |
| Russell 2000 | RUT |
| S&P/TSX Composite (Canada) | TSX |
| Bovespa (Brazil) | IBOV |
| IPC (Mexico) | MEXBOL |

**Europe**
| Index | Ticker |
|---|---|
| FTSE 100 (UK) | UKX |
| Euro Stoxx 50 | SX5E |
| DAX (Germany) | DAX |
| CAC 40 (France) | CAC |
| FTSE MIB (Italy) | FTSEMIB |
| IBEX 35 (Spain) | IBEX |
| SMI (Switzerland) | SMI |

**Asia-Pacific**
| Index | Ticker |
|---|---|
| Nikkei 225 (Japan) | NKY |
| Hang Seng (Hong Kong) | HSI |
| Shanghai Composite (China) | SHCOMP |
| CSI 300 (China) | CSI300 |
| KOSPI (South Korea) | KOSPI |
| S&P/ASX 200 (Australia) | AS51 |
| Sensex (India) | SENSEX |
| Nifty 50 (India) | NIFTY |
| Straits Times (Singapore) | STI |

**Sector Indices (US)**
| Index | Description |
|---|---|
| S&P 500 Financials | XLF sector |
| S&P 500 Technology | XLK sector |
| S&P 500 Energy | XLE sector |
| S&P 500 Healthcare | XLV sector |
| S&P 500 Industrials | XLI sector |
| S&P 500 Real Estate | XLRE sector |
| Philadelphia Semiconductor | SOX |

### Step 2: Fixed Income & Rates

**US Treasuries**
| Maturity | Data Points |
|---|---|
| 2-Year | Yield, daily change (bps) |
| 5-Year | Yield, daily change (bps) |
| 10-Year | Yield, daily change (bps) |
| 30-Year | Yield, daily change (bps) |
| 2s10s Spread | Spread (bps), daily change |
| 5s30s Spread | Spread (bps), daily change |

**Global Sovereign Yields (10-Year)**
- German Bund
- UK Gilt
- Japan JGB
- China CGB
- Italy BTP
- France OAT
- Australia ACG

**Credit Spreads**
| Measure | Source |
|---|---|
| IG CDX (North America) | Markit CDX.NA.IG |
| HY CDX (North America) | Markit CDX.NA.HY |
| iTraxx Europe Main | Markit iTraxx |
| iTraxx Europe Crossover | Markit iTraxx Xover |
| US IG OAS (ICE BofA) | Spread to Treasuries |
| US HY OAS (ICE BofA) | Spread to Treasuries |
| Leveraged Loan Index (S&P/LSTA) | Price, yield, spread |
| CLO AAA Spread | Spread to benchmark |
| CLO BBB Spread | Spread to benchmark |

**Money Markets & Central Bank Rates**
- Fed Funds Effective Rate
- SOFR
- Fed Funds Futures (next 3 meetings) — implied rate only, no probability interpretation
- ECB Deposit Facility Rate
- BoE Bank Rate
- BoJ Policy Rate

### Step 3: Commodities

| Commodity | Contract |
|---|---|
| WTI Crude Oil | Front-month futures |
| Brent Crude Oil | Front-month futures |
| Natural Gas (Henry Hub) | Front-month futures |
| Gold (spot) | XAU/USD |
| Silver (spot) | XAG/USD |
| Copper | LME 3-month |
| Iron Ore (Dalian) | Front-month |
| Wheat (CBOT) | Front-month |
| Corn (CBOT) | Front-month |
| Soybeans (CBOT) | Front-month |

### Step 4: Foreign Exchange

**Major Pairs**
| Pair | Description |
|---|---|
| EUR/USD | Euro vs Dollar |
| GBP/USD | Sterling vs Dollar |
| USD/JPY | Dollar vs Yen |
| USD/CHF | Dollar vs Swiss Franc |
| AUD/USD | Aussie vs Dollar |
| USD/CAD | Dollar vs Canadian |
| NZD/USD | Kiwi vs Dollar |

**EM & Other**
| Pair / Index | Description |
|---|---|
| DXY | US Dollar Index |
| USD/CNY | Dollar vs Renminbi |
| USD/INR | Dollar vs Rupee |
| USD/BRL | Dollar vs Real |
| USD/MXN | Dollar vs Peso |
| USD/ZAR | Dollar vs Rand |
| USD/TRY | Dollar vs Lira |
| Bitcoin (BTC/USD) | Spot price |
| Ethereum (ETH/USD) | Spot price |

### Step 5: Volatility & Flows

| Indicator | Description |
|---|---|
| VIX | CBOE Volatility Index |
| VIX Term Structure | Front vs 3-month spread |
| MOVE Index | Bond market volatility |
| VVIX | Vol-of-vol |
| Put/Call Ratio (CBOE Equity) | Daily ratio |
| US Equity Fund Flows (weekly) | Net flows, latest available |
| EM Fund Flows (weekly) | Net flows, latest available |

## Output Format

For each asset, report in a consistent table:

```
| Asset | Last | Change | % Change | WTD | MTD | YTD |
```

- Use exact closing values (not rounded beyond standard market convention)
- Positive changes: prefix with `+`
- Negative changes: prefix with `-`
- Rate changes in basis points (bps)
- Mark data as "Prior close" if markets have not yet opened for the day
- If a data point is unavailable, mark as `N/A` — never estimate or interpolate

## Data Sources

Use available MCP servers (Morningstar, LSEG, FactSet, S&P Global) as primary sources. Supplement with web search for any gaps. Always note the source and timestamp of data.
