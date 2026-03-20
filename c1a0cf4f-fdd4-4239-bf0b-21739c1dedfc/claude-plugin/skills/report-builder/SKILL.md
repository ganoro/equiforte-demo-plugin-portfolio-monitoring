---
name: report-builder
description: Assemble final intelligence content YAML files from collected market data, geopolitical developments, regulatory/ops intel, and event calendar data. Use when all daily brief data has been collected and needs to be formatted into the YAML deliverables for the Equiforte website.
---

# Intelligence Content Report Builder

Assemble the final intelligence content YAML files from collected data. Output three YAML files that follow the `intelligence-content` skill format exactly.

## CRITICAL: Output Rules

- **MUST** create output directories: `mkdir -p output/intelligence-data/{ticker,daily-brief,pulse}`
- **MUST** write three files using the Write tool:
  1. `output/intelligence-data/daily-brief/{date}.yaml`
  2. `output/intelligence-data/ticker/latest.yaml`
  3. `output/intelligence-data/pulse/{date}.yaml`
- **MUST** verify all files were written: `ls -la output/intelligence-data/daily-brief/*.yaml output/intelligence-data/ticker/*.yaml output/intelligence-data/pulse/*.yaml`
- **DO NOT** make any additional web searches or data lookups. Use only collected data.
- **DO NOT** add data beyond what was gathered. Mark gaps as `N/A`.

## File 1: Daily Brief YAML

Write to `output/intelligence-data/daily-brief/{YYYY-MM-DD}.yaml`:

```yaml
---
title: "Daily Brief — Month DD, YYYY"
date: "YYYY-MM-DD"
author: "Equiforte Intelligence"
status: published
summary: "Under 200 chars — headline numbers and key theme for homepage card."
preview: |
  <h3>Market Snapshot</h3>
  [Market data tables — equity indices, rates, credit, commodities, FX, vol]
  <h3>Regulatory Watch</h3>
  [2-4 regulatory items with deadlines and affected parties]

full_content: |
  <h3>Market Snapshot</h3>
  [Same content as preview Market Snapshot]
  <h3>Regulatory Watch</h3>
  [Same content as preview Regulatory Watch]
  <h3>Operational Intel</h3>
  [Fund admin, tech, vendor developments — 2-3 items]
  <h3>Data Snapshot</h3>
  [Key metrics table — 8-10 rows max]
  <h3>The CFO Take</h3>
  [3 actionable items as <ul> list, each derived from today's data]
  <h3>Coming This Week</h3>
  [Forward calendar as <ul> grouped by day]
```

### Market Snapshot Table Format

```html
<table>
  <tr><th>Index</th><th>Close</th><th>Change</th><th>% Change</th></tr>
  <tr><td>S&P 500</td><td>5,892</td><td>+23.45</td><td>+0.40%</td></tr>
</table>
```

Separate tables for: US Equities, International Equities, US Treasuries & Rates, Credit Spreads, Commodities, FX, Volatility. Or combine into one compact table if space is tight.

### The CFO Take Format

```html
<p><strong>3 things PE CFOs should be thinking about today:</strong></p>
<ul>
  <li><strong>Topic</strong> — Actionable guidance tied to today's data.</li>
  <li><strong>Topic</strong> — Actionable guidance tied to today's data.</li>
  <li><strong>Topic</strong> — Actionable guidance tied to today's data.</li>
</ul>
```

Each item MUST reference something reported in the brief. Start with an action verb.

## File 2: Ticker Banner YAML

Write to `output/intelligence-data/ticker/latest.yaml`:

```yaml
---
updated_at: "YYYY-MM-DDTHH:MM:SSZ"
separator: " • "
items:
  - text: "Metric ▲/▼ value — context"
    direction: up|down|neutral
```

Rules:
- 4-6 items, each under 80 characters
- Use ▲ for positive, ▼ for negative in the text
- Include metric name + direction + value
- Distill the most significant data points from the daily brief
- Mix of asset classes (equity, credit, rates, deals)

## File 3: Private Markets Pulse YAML

Write to `output/intelligence-data/pulse/{YYYY-MM-DD}.yaml`:

```yaml
---
title: "Private Markets Pulse — Month DD, YYYY"
date: "YYYY-MM-DD"
author: "Equiforte Intelligence"
status: published
summary: "Under 200 chars — PE/credit focused headline."
preview: |
  <h3>Today's Priority Signals</h3>
  [🔴 Action Required, 🟡 Monitor, 🟢 Opportunity — 1-2 each]
  <h3>Deep Dive: [Theme]</h3>
  [Opening paragraph of the deep dive]

full_content: |
  <h3>Today's Priority Signals</h3>
  [Same as preview]
  <h3>Deep Dive: [Theme]</h3>
  [Full deep dive — 3-5 paragraphs with "What's driving it" and "CFO implication"]
  <h3>LP/GP Signals</h3>
  [Fundraising, allocation changes, secondary market — 3-5 items as <ul>]
  <h3>Sector Spotlight: [Sector]</h3>
  [Rotating sector analysis with deal data table if available]
```

### Priority Signals Format

```html
<p>🔴 <strong>Action Required</strong> — What happened + deadline + what to do.</p>
<p>🟡 <strong>Monitor</strong> — Development to watch + why it matters.</p>
<p>🟢 <strong>Opportunity</strong> — Window + potential advantage + how to act.</p>
```

### Pulse Content Sources

Build the Pulse from the SAME collected data as the daily brief, but with PE/credit CFO lens:
- Priority signals: synthesize from regulatory, market, and deal data
- Deep dive: select the most significant PE/credit theme and expand
- LP/GP signals: extract from corporate/deal activity and any LP news
- Sector spotlight: rotate through Healthcare, Tech, Financial Services, Industrials, Consumer, Energy/Infrastructure

## Formatting Rules

- Positive: `+1.23` / `+0.45%`. Negative: `-1.23` / `-0.45%`. Unchanged: `Unchanged`
- Billions: `$12.3B`, Millions: `$456.7M`, bps: `+5 bps`
- All content as HTML within YAML multiline strings (`|`)
- **No interpretation**: state direction but never speculate on causes or use subjective words (bullish, bearish, surge, plunge, rally, selloff)

## Validation Checklist

- [ ] All three files written to correct paths
- [ ] All required YAML fields present (title, date, author, status, summary, preview, full_content)
- [ ] `status: published`
- [ ] `date` in YYYY-MM-DD format
- [ ] `summary` under 200 characters
- [ ] `preview` is substantial (50+ chars, 2-3 sections)
- [ ] `full_content` includes all preview content PLUS additional sections
- [ ] Ticker has 4-6 items, each under 80 chars, with valid direction values
- [ ] All HTML renders correctly (properly closed tags)
- [ ] No fabricated data — `N/A` for missing values
- [ ] No interpretive language
