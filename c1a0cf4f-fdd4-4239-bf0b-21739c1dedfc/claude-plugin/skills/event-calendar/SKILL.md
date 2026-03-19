---
name: event-calendar
description: Compile upcoming financial events, economic releases, earnings, conferences, central bank meetings, and deal milestones. Use when generating a daily brief or when the user asks about upcoming events, the economic calendar, or conference schedules.
---

# Event Calendar

Compile a forward-looking calendar of scheduled events relevant to financial professionals. All dates/times in Eastern Time (ET).

## CRITICAL: Search Efficiency Rules

You have a **budget of 6 web searches maximum** for this entire skill.

- **DO NOT** search for individual company earnings one by one
- **DO NOT** search for each central bank meeting date separately
- **DO NOT** search for conferences by individual bank/organizer
- **DO** use aggregator searches that return calendar/list pages
- Only cover **this week + next week**. Do not look further ahead except for major conferences.

### Recommended Search Strategy (6 searches)

1. **Search 1 — Economic calendar this week and next**: "economic calendar this week next week [date range] US Europe" → most aggregator sites return a full 2-week view
2. **Search 2 — Central bank meeting schedule**: "central bank meeting schedule 2026 Fed ECB BoE BoJ" → all meeting dates in one search (these are published for the full year)
3. **Search 3 — Earnings calendar this week**: "earnings calendar this week [date] S&P 500 major companies reporting" → aggregator page with all names
4. **Search 4 — Earnings calendar next week**: "earnings calendar next week [date range] major companies" → same approach
5. **Search 5 — Investor conferences and events**: "investor conferences financial events [month] [year]" → conference aggregator
6. **Search 6 — IPO calendar and Treasury auctions**: "IPO calendar upcoming Treasury auction schedule [month] [year]"

## What to Collect

### Economic Calendar (This Week + Next Week)

**High-importance only** — do not list every minor release:
- US: NFP, CPI, PPI, PCE, GDP, FOMC, retail sales, ISM, jobless claims
- Europe: ECB decision, Eurozone CPI, GDP, PMIs
- UK: BoE decision, CPI, PMIs
- China: PBoC, CPI, PMIs, trade balance
- Japan: BoJ, CPI, Tankan

Format:
| Date | Time (ET) | Country | Indicator | Period | Prior | Consensus |

### Central Bank Calendar

| Bank | Next Meeting | Rate Decision Expected |

Cover: FOMC, ECB, BoE, BoJ, PBoC, RBA, BoC. Others only if returned by search.

### Earnings Calendar

**This week and next week only.** Focus on:
- S&P 500 constituents
- Sector bellwethers
- Do not list companies with market cap below $10B unless sector-relevant

Format:
| Date | Time | Company | Ticker | EPS Est | Rev Est |

### Conferences & Events (Next 4 Weeks)

Only list events found in a single search. Do not search for individual conference organizers.

| Dates | Event | Location | Key Sectors |

### IPO & Issuance Calendar

- Upcoming IPOs (if found)
- US Treasury auction schedule for the week
- Notable IG/HY issuance expected

### Options/Index Dates

Only mention if this week or next includes: monthly/quarterly options expiry, index rebalancing (Russell, MSCI, S&P), or triple/quad witching.

## Output Format

**This week**: Day-by-day with all categories merged per day.
**Next week**: Grouped by category, dates noted.

- `[TBD]` for tentative dates
- `N/A` for unavailable consensus
- Never fabricate dates or estimates

## Data Sources

Use MCP servers (FactSet, Morningstar, S&P Global, MT Newswires, PitchBook) for calendars. Web search for conferences and IPOs.
