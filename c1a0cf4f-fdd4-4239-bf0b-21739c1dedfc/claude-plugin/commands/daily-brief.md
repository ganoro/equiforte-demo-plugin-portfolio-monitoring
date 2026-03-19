---
name: daily-brief
description: Generate a comprehensive daily market briefing with global indices, rates, commodities, FX, economic data, geopolitical developments, and upcoming events. Facts and data only — no editorial interpretation.
arguments:
  - name: focus
    description: "Optional focus area: 'pe' (private equity), 'pd' (private debt / credit), 'hf' (hedge funds), 'ib' (investment banking), or 'all' (default). Adjusts which sections are emphasized."
    required: false
  - name: date
    description: "Date for the briefing (YYYY-MM-DD). Defaults to today."
    required: false
  - name: output
    description: "Output path for the markdown report file. Defaults to ./daily-brief-{date}.md"
    required: false
---

# Daily Market Brief

Generate a daily market briefing report for **{{ focus | default: "all" }}** professionals as of **{{ date | default: "today" }}**.

## CRITICAL: Efficiency Constraints

This brief must complete within **5 minutes**. Total web searches across all skills: **maximum 20**.

- Market snapshot: max 8 searches
- Geopolitical monitor: max 6 searches
- Event calendar: max 6 searches
- Report assembly: 0 searches (uses only collected data)

**DO NOT** re-search for data you already have. **DO NOT** search for individual assets one at a time. Use broad queries that return summary/dashboard pages. Accept the precision available from summary pages. Mark gaps as `N/A` rather than retrying.

## Instructions

Gather data using these skills, then assemble the report:

1. **market-snapshot** — global equity indices, rates, credit spreads, commodities, FX, volatility
2. **geopolitical-monitor** — central bank actions, economic data releases, geopolitical/trade/policy developments, major corporate events
3. **event-calendar** — upcoming economic calendar, central bank meetings, earnings, conferences, IPOs, auctions

**Important — avoid cross-task duplication:**
- Central bank **actions that already happened today** → geopolitical-monitor only
- Central bank **upcoming meeting dates** → event-calendar only
- Economic data **already released today** → geopolitical-monitor only
- Economic data **scheduled for future dates** → event-calendar only

4. **report-builder** — assemble all collected data into the final markdown report. No additional searches.

## Focus Area Guidance

- **all**: Full briefing across all sections with equal weight.
- **pe**: Emphasize M&A activity, leveraged loan / HY markets, sponsor-backed deal flow, PE conferences.
- **pd**: Emphasize credit spreads, leveraged loan indices, CLO markets, default rates, direct lending.
- **hf**: Emphasize volatility, flows, positioning, factor performance, cross-asset momentum.
- **ib**: Emphasize ECM/DCM issuance, M&A announced/closed, IPO pipeline, sector deal activity.

## Output

Write the completed report to **{{ output | default: "./daily-brief-{date}.md" }}**.

Facts, data, and sourced statistics only. No opinions, forecasts, or subjective interpretation.
