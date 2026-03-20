---
name: Intelligence Content System
description: This skill should be used when the user asks to "generate daily brief", "create intelligence content", "publish ticker", "create pulse report", "write CFO insights", "generate YAML content", "update ticker banner", "write morning briefing", "create market update", or mentions intelligence content, daily-brief YAML, pulse YAML, or cfo-insights YAML. Provides the mandatory output format and structure for all Equiforte intelligence content types.
---

# Intelligence Content System

Generate structured YAML content files for the Equiforte intelligence platform. All intelligence content is delivered as YAML files with HTML-formatted `preview` and `full_content` fields. The website auto-refreshes every 10 minutes after a push.

## Content Types Overview

| Type | Directory | Filename | Purpose |
|------|-----------|----------|---------|
| Ticker Banner | `ticker/` | `latest.yaml` | Homepage scrolling banner |
| Daily Brief | `daily-brief/` | `YYYY-MM-DD.yaml` | Morning market briefing |
| Private Markets Pulse | `pulse/` | `YYYY-MM-DD.yaml` | PE/credit-focused analysis |
| CFO Insights | `cfo-insights/` | `YYYY-MM-DD-topic.yaml` | Survey results & research |

## Output Directory Structure

All generated content MUST be written to `output/` with the intelligence-data subdirectory structure:

```
output/
└── intelligence-data/
    ├── ticker/
    │   └── latest.yaml
    ├── daily-brief/
    │   └── YYYY-MM-DD.yaml
    └── pulse/
        └── YYYY-MM-DD.yaml
```

Create directories first: `mkdir -p output/intelligence-data/{ticker,daily-brief,pulse,cfo-insights}`

## YAML Structure (All Article Types)

Every article YAML file (daily-brief, pulse, cfo-insights) MUST contain these required fields:

```yaml
---
title: "Article Title — Month DD, YYYY"
date: "YYYY-MM-DD"
author: "Equiforte Intelligence"
status: published
summary: "One-line summary for homepage card (under 200 chars)."
preview: |
  <h3>Section Heading</h3>
  <p>Content visible to everyone — no registration required.</p>
  <p>Include 2-3 sections to give readers a taste.</p>

full_content: |
  <h3>Section Heading</h3>
  <p>Same content as preview, plus additional gated sections.</p>
  <h3>Additional Section</h3>
  <p>Requires email registration to read.</p>
```

### Content Gating Rules

- `preview` — always visible, no registration needed. Include 2-3 substantial sections.
- `full_content` — requires work email registration. MUST include the preview content PLUS additional sections.
- Registration subscribes to newsletter (`intelligence_gate` source).

## Ticker Banner Format

The ticker uses a different structure. See `references/yaml-formats.md` for the full schema.

```yaml
---
updated_at: "2026-03-20T08:00:00Z"
separator: " • "
items:
  - text: "PE Deal Volume ▲ 12% Q4 2025 — $197B deployed"
    direction: up
```

Rules: 4-6 items, each under 80 characters. Use ▲/▼ in text. Direction: `up`, `down`, or `neutral`.

## Formatting in Content Fields

The `preview` and `full_content` fields support:
- `<h3>`, `<h4>` for section headings
- `<p>` for paragraphs
- `<ul>`, `<li>` for lists
- `<table>`, `<tr>`, `<th>`, `<td>` for data tables
- `<strong>`, `<em>` for emphasis
- `<blockquote>` for quotes
- Emoji indicators: 🔴 Action Required, 🟡 Monitor, 🟢 Opportunity

## Standard Sections by Content Type

### Daily Brief Sections
1. **Market Snapshot** — rates, spreads, deal activity (tables)
2. **Regulatory Watch** — new rules, deadlines, guidance
3. **Operational Intel** — fund admin, technology, vendor news
4. **Data Snapshot** — key metrics table
5. **The CFO Take** — 3 things to think about today
6. **Coming This Week** — upcoming events and data releases

### Private Markets Pulse Sections
1. **Today's Priority Signals** — 🔴 Action Required, 🟡 Monitor, 🟢 Opportunity
2. **Deep Dive** — detailed analysis of one theme
3. **LP/GP Signals** — relationship and fundraising intelligence
4. **Sector Spotlight** — rotating sector analysis

### CFO Insights Sections
1. **Survey Highlights** — headline findings with percentages
2. **Category Breakdowns** — AI adoption, reporting, regulatory, etc.
3. **CFO Verbatims** — direct quotes from respondents
4. **Methodology** — sample size, respondent profile, dates

## Validation Rules

Before writing output, validate:

| Check | Severity | Rule |
|-------|----------|------|
| Required fields present | Error | title, date, author, status, summary, preview, full_content |
| Status value | Error | Must be `published` or `draft` |
| Date format | Error | Must be `YYYY-MM-DD` |
| Ticker items | Error | Each needs `text` and `direction` (up/down/neutral) |
| Preview length | Warning | At least 50 characters |
| Full content > preview | Warning | full_content should be longer than preview |
| Summary length | Warning | Under 200 characters |
| Ticker item length | Warning | Under 80 characters per item |
| Ticker item count | Warning | Under 8 items |

## Workflow

1. Gather data using research skills (market-snapshot, geopolitical-monitor, event-calendar, regulatory-ops-intel)
2. Structure findings into the standard sections for the content type
3. Format section content as HTML
4. Build the YAML file with all required fields
5. Write the `preview` with the first 2-3 sections (ungated)
6. Write `full_content` with ALL sections including preview content
7. Always use today's date for `date` and `updated_at` fields — never hardcode a past date
8. Generate the ticker from the most significant data points
9. Write files to `output/intelligence-data/` with correct filenames
10. Verify files exist and are non-empty

## Additional Resources

### Reference Files

- **`references/yaml-formats.md`** — Complete YAML schemas with full examples for all four content types
- **`references/content-sections.md`** — Detailed guidance for writing each section, with HTML formatting examples and quality criteria
