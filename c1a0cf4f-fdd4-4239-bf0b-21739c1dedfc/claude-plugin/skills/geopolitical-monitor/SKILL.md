---
name: geopolitical-monitor
description: Monitor and compile geopolitical and macroeconomic developments relevant to financial markets. Use when generating a daily brief or when the user asks about geopolitical risks, macro developments, or market-moving events.
---

# Geopolitical & Macro Monitor

Compile today's geopolitical and macroeconomic developments relevant to financial markets. Report only confirmed facts with sources. No speculation.

## CRITICAL: Search Efficiency Rules

You have a **budget of 6 web searches maximum** for this entire skill.

- **DO NOT** search for every central bank individually
- **DO NOT** search for speculative or tangential geopolitical topics
- **DO NOT** search for topics already covered by the event-calendar skill (upcoming economic releases, earnings, conferences)
- **DO** use broad financial news summary searches that cover multiple topics per query
- Only report what your searches actually return — do not go hunting for stories

### Recommended Search Strategy (6 searches)

1. **Search 1 — Top market-moving news**: "financial markets news today [date] major developments" → captures the biggest stories across all categories
2. **Search 2 — Central bank actions today**: "central bank decisions speeches today Fed ECB BoE BoJ [date]" → all central bank activity in one search
3. **Search 3 — Economic data released today**: "economic data releases today [date] CPI GDP PMI jobless claims" → all data releases in one search
4. **Search 4 — Geopolitical/trade/policy**: "geopolitical developments tariffs trade policy sanctions today [date]" → trade, fiscal, geopolitical events
5. **Search 5 — Major M&A and corporate news**: "major M&A deals corporate news defaults IPO today [date]" → deal activity, defaults, rating changes
6. **Search 6 — Energy/commodity supply developments**: "OPEC oil supply energy commodity developments today [date]" → only if Search 1 or 4 suggests something noteworthy; otherwise skip

## What to Report

### Central Bank & Monetary Policy (from Search 2)
- Rate decisions, speeches, minutes releases from today only
- Include direct quotes for key policy language
- **Do not** separately search for minor central banks (SNB, Riksbank, Norges, etc.) — include only if returned

### Economic Data Releases (from Search 3)
For each release:
| Time (ET) | Country | Indicator | Period | Actual | Prior | Consensus | Surprise |

### Fiscal, Regulatory & Trade Policy (from Search 4)
- Only report confirmed actions: executive orders, tariff changes, sanctions, legislation passed
- State what happened, when, and which sectors/assets are directly affected

### Geopolitical Events (from Searches 1, 4)
- Only report developments confirmed by official sources or multiple credible outlets
- **Scope limit**: Only include if there is a clear, direct financial market impact (commodity prices, trade flows, sanctions, currency). Skip general political news.

### Corporate & Deal Activity (from Search 5)
- M&A announcements >$1B
- Major defaults, restructurings, or rating changes
- IPO pricings
- CEO departures at S&P 500 companies

## Output Format

Organize into sections. Each item:

```
**[TIME ET] [HEADLINE]**
[1-2 sentence factual description]. Source: [source name].
```

- If a section has no developments, state "No significant developments"
- Do not omit sections
- `[BREAKING]` only if within last 2 hours

## Data Sources

Use MT Newswires MCP server as primary. Web search to supplement. Cross-reference with official websites for policy actions.
