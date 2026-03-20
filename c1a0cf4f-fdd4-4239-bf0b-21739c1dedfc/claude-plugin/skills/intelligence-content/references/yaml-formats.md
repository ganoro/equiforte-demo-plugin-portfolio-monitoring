# Intelligence Content YAML Formats

Complete schemas and examples for all four intelligence content types.

## 1. Ticker Banner (`ticker/latest.yaml`)

The scrolling banner on the homepage. Always overwrite `latest.yaml` — not versioned by date.

### Schema

```yaml
---
updated_at: "YYYY-MM-DDTHH:MM:SSZ"   # Required — ISO timestamp
separator: " • "                       # Optional — default " • "
items:                                 # Required — array of 4-6 items
  - text: "string"                     # Required — under 80 chars
    direction: "up|down|neutral"       # Required
```

### Full Example

```yaml
---
updated_at: "2026-03-20T08:00:00Z"
separator: " • "
items:
  - text: "PE Deal Volume ▲ 12% Q4 2025 — $197B deployed"
    direction: up
  - text: "Private Credit Spreads ▼ tightening — L+475 avg"
    direction: down
  - text: "VC Fundraising ▲ rebounds — $68B raised in Q1 2026"
    direction: up
  - text: "GP Stake Sales ▲ 3 new deals this week"
    direction: up
  - text: "CLO Issuance ▼ $8.2B — below 4-week avg"
    direction: down
```

### Ticker Content Guidelines

- Distill the most market-moving data points from the daily brief
- Include metric name, direction symbol (▲/▼), and value
- Mix positive and negative indicators for balance
- Supported Unicode: ▲ ▼ → ← • — ● ■ ★ $ % + -

## 2. Daily Brief (`daily-brief/YYYY-MM-DD.yaml`)

### Schema

```yaml
---
title: "string"           # Required — "Daily Brief — Month DD, YYYY"
date: "YYYY-MM-DD"        # Required
author: "string"          # Required — "Equiforte Intelligence"
status: "published|draft" # Required
summary: "string"         # Required — under 200 chars, for homepage card
preview: |                # Required — HTML, visible to all (ungated)
  ...
full_content: |           # Required — HTML, visible after email registration
  ...
```

### Full Example

```yaml
---
title: "Daily Brief — March 20, 2026"
date: "2026-03-20"
author: "Equiforte Intelligence"
status: published
summary: "Fed holds rates steady; PE deal volume rises 12% in Q4; CLO spreads tighten as demand outpaces supply."
preview: |
  <h3>Market Snapshot</h3>
  <table>
    <tr><th>Index</th><th>Close</th><th>Change</th><th>% Change</th></tr>
    <tr><td>S&P 500</td><td>5,892.14</td><td>+23.45</td><td>+0.40%</td></tr>
    <tr><td>US 10Y</td><td>4.28%</td><td>-3 bps</td><td>—</td></tr>
    <tr><td>HY OAS</td><td>342 bps</td><td>-5 bps</td><td>—</td></tr>
    <tr><td>WTI Crude</td><td>$71.23</td><td>+$0.87</td><td>+1.24%</td></tr>
    <tr><td>DXY</td><td>103.45</td><td>-0.32</td><td>-0.31%</td></tr>
  </table>

  <h3>Regulatory Watch</h3>
  <p><strong>SEC Proposed Rule on Fund Fee Transparency</strong> — Comment period opens for new disclosure requirements on management fee offsets and carried interest calculations. Affects PE funds with >$500M AUM. Deadline: May 15, 2026.</p>
  <p><strong>EU AIFMD II Implementation</strong> — Updated guidelines on loan origination by alternative funds take effect April 1. Impacts credit funds with EU LPs.</p>

full_content: |
  <h3>Market Snapshot</h3>
  <table>
    <tr><th>Index</th><th>Close</th><th>Change</th><th>% Change</th></tr>
    <tr><td>S&P 500</td><td>5,892.14</td><td>+23.45</td><td>+0.40%</td></tr>
    <tr><td>US 10Y</td><td>4.28%</td><td>-3 bps</td><td>—</td></tr>
    <tr><td>HY OAS</td><td>342 bps</td><td>-5 bps</td><td>—</td></tr>
    <tr><td>WTI Crude</td><td>$71.23</td><td>+$0.87</td><td>+1.24%</td></tr>
    <tr><td>DXY</td><td>103.45</td><td>-0.32</td><td>-0.31%</td></tr>
  </table>

  <h3>Regulatory Watch</h3>
  <p><strong>SEC Proposed Rule on Fund Fee Transparency</strong> — Comment period opens for new disclosure requirements on management fee offsets and carried interest calculations. Affects PE funds with >$500M AUM. Deadline: May 15, 2026.</p>
  <p><strong>EU AIFMD II Implementation</strong> — Updated guidelines on loan origination by alternative funds take effect April 1. Impacts credit funds with EU LPs.</p>

  <h3>Operational Intel</h3>
  <p><strong>Allvue Systems acquires eFront analytics module</strong> — Consolidation in PE tech stack continues. Migration timeline: Q3 2026 for existing eFront clients.</p>
  <p><strong>ILPA releases updated DDQ template v4.0</strong> — New sections on AI usage, cybersecurity controls, and DEI metrics. Expect LP adoption in Q2 fundraising cycles.</p>

  <h3>Data Snapshot</h3>
  <table>
    <tr><th>Metric</th><th>Current</th><th>Change</th></tr>
    <tr><td>Fed Funds Rate</td><td>4.25-4.50%</td><td>Unchanged</td></tr>
    <tr><td>US IG OAS</td><td>98 bps</td><td>-2 bps</td></tr>
    <tr><td>US HY OAS</td><td>342 bps</td><td>-5 bps</td></tr>
    <tr><td>S&P/LSTA Lev Loan</td><td>96.82</td><td>+0.15</td></tr>
    <tr><td>PE Deal Count (MTD)</td><td>127</td><td>+14% vs prior month</td></tr>
  </table>

  <h3>The CFO Take</h3>
  <p><strong>3 things PE CFOs should be thinking about today:</strong></p>
  <ul>
    <li><strong>Fee disclosure prep</strong> — Start cataloging management fee offset arrangements ahead of SEC comment period. Proactive disclosure reduces LP friction.</li>
    <li><strong>CLO refinancing window</strong> — Tighter spreads create a 4-6 week window to refinance existing CLO tranches. Coordinate with your credit team on warehouse facilities.</li>
    <li><strong>DDQ template refresh</strong> — ILPA v4.0 adds AI and cyber sections. Update your DDQ responses now before Q2 fundraising meetings.</li>
  </ul>

  <h3>Coming This Week</h3>
  <ul>
    <li><strong>Thursday</strong> — Initial Jobless Claims (8:30 ET), Existing Home Sales (10:00 ET)</li>
    <li><strong>Friday</strong> — PMI Flash (9:45 ET), New Home Sales (10:00 ET)</li>
    <li><strong>Next Monday</strong> — Durable Goods Orders (8:30 ET)</li>
  </ul>
```

## 3. Private Markets Pulse (`pulse/YYYY-MM-DD.yaml`)

Same YAML schema as Daily Brief (title, date, author, status, summary, preview, full_content). Different standard sections.

### Full Example

```yaml
---
title: "Private Markets Pulse — March 20, 2026"
date: "2026-03-20"
author: "Equiforte Intelligence"
status: published
summary: "CLO spreads tighten as demand surges; GP stake market heats up with 3 new deals; healthcare PE exits accelerate."
preview: |
  <h3>Today's Priority Signals</h3>
  <p>🔴 <strong>Action Required</strong> — SEC fee transparency rule comment period opens. Review management fee offset disclosures with counsel before May 15 deadline.</p>
  <p>🟡 <strong>Monitor</strong> — CLO AAA spreads at 6-month tights (SOFR+135). Refinancing window may narrow if supply picks up next week.</p>
  <p>🟢 <strong>Opportunity</strong> — GP stake secondary market seeing increased LP demand. Three new platform deals announced this week at 12-15x trailing management fees.</p>

  <h3>Deep Dive: CLO Market Reset</h3>
  <p>CLO issuance hit $8.2B this week, below the 4-week rolling average of $9.1B, yet spreads continued to tighten across the capital stack...</p>

full_content: |
  <h3>Today's Priority Signals</h3>
  <p>🔴 <strong>Action Required</strong> — SEC fee transparency rule comment period opens. Review management fee offset disclosures with counsel before May 15 deadline.</p>
  <p>🟡 <strong>Monitor</strong> — CLO AAA spreads at 6-month tights (SOFR+135). Refinancing window may narrow if supply picks up next week.</p>
  <p>🟢 <strong>Opportunity</strong> — GP stake secondary market seeing increased LP demand. Three new platform deals announced this week at 12-15x trailing management fees.</p>

  <h3>Deep Dive: CLO Market Reset</h3>
  <p>CLO issuance hit $8.2B this week, below the 4-week rolling average of $9.1B, yet spreads continued to tighten across the capital stack. AAA tranches priced at SOFR+135, down from SOFR+155 a month ago.</p>
  <p><strong>What's driving it:</strong> Demand from Japanese banks and US insurance companies is outpacing new supply. The bid-to-cover ratio on recent deals averaged 2.8x.</p>
  <p><strong>CFO implication:</strong> Funds with warehouse facilities should evaluate refinancing existing CLO tranches in the next 4-6 weeks before the Q2 issuance calendar fills up.</p>

  <h3>LP/GP Signals</h3>
  <ul>
    <li><strong>CalPERS</strong> increased alternatives allocation target to 35% (from 33%), with emphasis on infrastructure and private credit.</li>
    <li><strong>ADIA</strong> launching $2B co-investment vehicle focused on European mid-market buyouts.</li>
    <li><strong>Secondary market</strong> — LP portfolio sales at 92-95 cents on the dollar for 2019-2021 vintage buyout funds.</li>
  </ul>

  <h3>Sector Spotlight: Healthcare Services</h3>
  <p><strong>Exit activity accelerating</strong> — 4 PE-backed healthcare platforms announced exits this month, up from 1 in February.</p>
  <table>
    <tr><th>Company</th><th>Sponsor</th><th>Exit Type</th><th>EV</th><th>Multiple</th></tr>
    <tr><td>MedVet Partners</td><td>KKR</td><td>Secondary</td><td>$3.2B</td><td>18x EBITDA</td></tr>
    <tr><td>ClearPath Diagnostics</td><td>Welsh Carson</td><td>IPO</td><td>$2.1B</td><td>22x EBITDA</td></tr>
  </table>
```

## 4. CFO Insights (`cfo-insights/YYYY-MM-DD-topic.yaml`)

Same YAML schema. Filename includes topic slug: `YYYY-MM-DD-topic.yaml`.

### Example

```yaml
---
title: "CFO Insights — Q1 2026 AI Adoption Survey"
date: "2026-03-20"
author: "Equiforte Intelligence"
status: published
summary: "67% of PE CFOs now use AI for portfolio monitoring; only 23% have formal AI governance policies."
preview: |
  <h3>Survey Highlights</h3>
  <p><strong>67%</strong> of PE CFOs report using AI tools for portfolio monitoring and reporting, up from 41% in Q1 2025.</p>
  <p><strong>78%</strong> plan to increase technology spend in 2026, with AI and data infrastructure as top priorities.</p>
  <p><strong>Only 23%</strong> have formal AI governance policies in place, citing uncertainty about regulatory requirements.</p>

full_content: |
  <h3>Survey Highlights</h3>
  <p><strong>67%</strong> of PE CFOs report using AI tools for portfolio monitoring and reporting, up from 41% in Q1 2025.</p>
  <p><strong>78%</strong> plan to increase technology spend in 2026, with AI and data infrastructure as top priorities.</p>
  <p><strong>Only 23%</strong> have formal AI governance policies in place, citing uncertainty about regulatory requirements.</p>

  <h3>Category Breakdowns</h3>
  <h4>AI Adoption</h4>
  <table>
    <tr><th>Use Case</th><th>Adoption Rate</th><th>YoY Change</th></tr>
    <tr><td>Portfolio monitoring dashboards</td><td>67%</td><td>+26 pts</td></tr>
    <tr><td>LP report generation</td><td>52%</td><td>+18 pts</td></tr>
    <tr><td>Due diligence research</td><td>45%</td><td>+22 pts</td></tr>
    <tr><td>Compliance/regulatory</td><td>31%</td><td>+12 pts</td></tr>
  </table>

  <h3>CFO Verbatims</h3>
  <blockquote>"We're using AI to cut LP report turnaround from 3 weeks to 5 days. The accuracy is surprisingly good once you train it on your data model." — CFO, mid-market buyout fund ($4B AUM)</blockquote>
  <blockquote>"My concern isn't whether AI works — it's whether our LPs will accept AI-generated analysis without human review. We need governance first." — CFO, growth equity fund ($2B AUM)</blockquote>

  <h3>Methodology</h3>
  <p><strong>Sample:</strong> 142 PE CFOs and Controllers across North America and Europe.</p>
  <p><strong>Fund sizes:</strong> $500M — $25B AUM. Mix of buyout (48%), growth (27%), credit (15%), venture (10%).</p>
  <p><strong>Survey period:</strong> February 1-28, 2026.</p>
  <p><strong>Response rate:</strong> 34% of invited participants.</p>
```

## File Naming Convention Summary

| Type | Pattern | Example |
|------|---------|---------|
| Ticker | `latest.yaml` (always) | `ticker/latest.yaml` |
| Daily Brief | `YYYY-MM-DD.yaml` | `daily-brief/2026-03-20.yaml` |
| Pulse | `YYYY-MM-DD.yaml` | `pulse/2026-03-20.yaml` |
| CFO Insights | `YYYY-MM-DD-topic.yaml` | `cfo-insights/2026-03-q1-survey.yaml` |

The latest article by filename sort is automatically shown on the homepage and `/latest` pages.
