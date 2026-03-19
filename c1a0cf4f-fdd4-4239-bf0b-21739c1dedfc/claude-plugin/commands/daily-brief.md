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

## Instructions

1. Use the **market-snapshot** skill to gather all global market data: equity indices, fixed income / rates, commodities, FX, and volatility indicators.
2. Use the **geopolitical-monitor** skill to compile today's geopolitical and macro developments that are relevant to financial markets.
3. Use the **event-calendar** skill to gather upcoming economic releases, earnings, conferences, central bank meetings, and deal/regulatory milestones.
4. Use the **report-builder** skill to assemble the final markdown report from all gathered data.

## Focus Area Guidance

- **all**: Full briefing across all sections with equal weight.
- **pe** (Private Equity): Emphasize M&A activity, leveraged loan / high yield markets, private market benchmarks, sponsor-backed deal flow, and PE-relevant conferences.
- **pd** (Private Debt / Credit): Emphasize credit spreads, leveraged loan indices, CLO markets, default rates, distressed names, direct lending benchmarks, and credit conferences.
- **hf** (Hedge Funds): Emphasize equity market microstructure (short interest, flows, positioning), volatility surfaces, cross-asset momentum, factor performance, and macro catalysts.
- **ib** (Investment Banking): Emphasize ECM/DCM issuance, M&A announced/closed, IPO pipeline, league table shifts, and sector deal activity.

## Output

Write the completed report to **{{ output | default: "./daily-brief-{date}.md" }}**.

The report must contain **only facts, data, and sourced statistics**. No opinions, forecasts, or subjective interpretation. Where a number moves up or down, state the direction and magnitude — nothing more.
