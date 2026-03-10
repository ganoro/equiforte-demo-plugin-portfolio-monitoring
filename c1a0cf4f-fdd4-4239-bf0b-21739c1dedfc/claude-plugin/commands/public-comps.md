---
name: public-comps
description: Analyze public market comparables — trading multiples, stock performance, and read-through to portfolio companies
tags:
  - public-comps
  - comparables
  - multiples
  - stock-market
  - valuation
placeholder: "e.g. Public comps for our healthcare portcos, or Show me all key comps for Fund III portfolio"
defaultOutput: Spreadsheet
icon: IconChartLine
arguments:
  - name: scope
    description: "Portfolio company, sector, fund, or 'all' for full portfolio"
    required: true
  - name: comps
    description: "Specific public companies to include (comma-separated tickers). e.g. 'MSFT, CRM, NOW'"
    required: false
---

# /public-comps — Public Market Comparables Analysis

Analyze public market comparables and their implications for portfolio company valuations.

## Parameters

- **Scope**: $ARGUMENTS
- **Additional comps**: (from arguments, if provided)

## Efficiency Rules (TARGET: 600 seconds)

- Batch all web searches — max 5-8 searches total
- Use financial data aggregators, not individual stock lookups
- One consolidated comps table, not separate analyses per company
- Focus on the 3-5 most relevant comps per portco, not exhaustive lists

## Instructions

### Step 1 — Identify Comparable Companies

For each portfolio company in scope, identify 3-5 key public comparables based on:
- Business model similarity
- End market overlap
- Revenue scale proximity
- Growth profile similarity

If user specifies additional comps, include them.

### Step 2 — Comp Universe Summary

| Public Comp | Ticker | Market Cap | Enterprise Value | LTM Revenue | LTM EBITDA | Revenue Growth | EBITDA Margin | Mapped Portco(s) |
|-------------|--------|-----------|-----------------|-------------|------------|----------------|---------------|-------------------|

### Step 3 — Trading Multiples

| Public Comp | Ticker | EV/Revenue (LTM) | EV/Revenue (NTM) | EV/EBITDA (LTM) | EV/EBITDA (NTM) | P/E | PEG Ratio |
|-------------|--------|-------------------|-------------------|------------------|------------------|-----|-----------|

Include: median, mean, high, low for each comp set.

### Step 4 — Stock Market Performance

| Public Comp | Ticker | YTD Return | 1Y Return | 3Y CAGR | 52W High/Low | Current vs. 52W High | Beta |
|-------------|--------|-----------|----------|---------|-------------|---------------------|------|

### Step 5 — Key Multiple Impact on Portco Valuations

For each portfolio company, show how public comp multiple movements affect marks:

| Portco | Current Mark Multiple | Public Comp Median | Premium/(Discount) | If Comp Median Applied | NAV Impact ($) | NAV Impact (%) |
|--------|----------------------|--------------------|--------------------|----------------------|---------------|----------------|

### Step 6 — Sector Trends & Read-Through

For each relevant sector, summarize:
- Recent earnings themes from public comps (guidance revisions, margin commentary)
- Sector-level tailwinds/headwinds
- M&A activity and strategic premium indicators
- How these trends apply to portfolio companies

Source: attribute to analyst reports (Goldman, Morgan Stanley, JP Morgan, Barclays, etc.) with dates.

### Step 7 — Monitoring Watchlist

Create an ongoing watchlist:

| Comp | Ticker | Watch For | Trigger Event | Next Earnings | Relevance to Portco |
|------|--------|----------|---------------|---------------|---------------------|

### Step 8 — Generate Output

Save to `output/public-comps-[scope]-[date].xlsx` with tabs:
- Comp Universe
- Trading Multiples
- Stock Performance
- Portco Impact
- Sector Trends

Offer PPTX for IC/board format.

## Adjustability

- Users can add/remove specific comps at any time
- Users can override which comps map to which portcos
- Users can request specific metrics or time periods
- Premium/discount to public comps can be set by user

## Critical Rules

- All market data must include the as-of date (intraday data = specify time)
- Source all financial data to provider (Bloomberg, Capital IQ, Yahoo Finance, etc.)
- Clearly state when using LTM vs. NTM multiples
- Don't conflate EV-based and equity-based multiples
- Note liquidity/size discount when comparing to private portcos
- Flag any comps with recent M&A rumors or pending transactions
- Include consensus estimates source when using forward multiples

## Workspace Rules (MANDATORY)

1. Run `mkdir -p output _research` first
2. All deliverables to `output/` only
3. Use relative paths only
