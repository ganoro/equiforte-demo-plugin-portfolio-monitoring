---
name: geopolitical-monitor
description: Monitor and compile geopolitical and macroeconomic developments relevant to financial markets. Use when generating a daily brief or when the user asks about geopolitical risks, macro developments, or market-moving events.
---

# Geopolitical & Macro Monitor

Compile today's geopolitical and macroeconomic developments that are relevant to financial markets. Report only confirmed facts with sources. No speculation on future outcomes.

## Data Collection Workflow

### Step 1: Central Bank & Monetary Policy

Collect any developments from the past 24 hours:

- **Federal Reserve**: Speeches, minutes releases, policy statements, emergency actions
- **European Central Bank**: Speeches, policy decisions, published research
- **Bank of England**: MPC statements, speeches, published analysis
- **Bank of Japan**: Policy decisions, yield curve control adjustments, governor statements
- **People's Bank of China**: Rate decisions, RRR changes, liquidity operations, fixing rates
- **Other major central banks**: RBA, Bank of Canada, SNB, Riksbank, Norges Bank, RBI, BCB

For each item report:
- Who spoke / what was released
- Exact quotes where market-relevant (no paraphrasing of policy language)
- Time of release / speech

### Step 2: Economic Data Releases (Today)

For each release that has already occurred today:

| Field | Description |
|---|---|
| Time (ET) | Release time |
| Country | Issuing country |
| Indicator | Official name |
| Period | Reference period |
| Actual | Released value |
| Prior | Previous period value |
| Consensus | Bloomberg/Reuters consensus |
| Surprise | Actual minus consensus |

Key releases to track:
- GDP (advance, preliminary, final)
- Employment / payrolls / unemployment rate
- CPI / PPI / PCE inflation
- PMI (manufacturing, services, composite)
- Retail sales
- Industrial production
- Housing starts / existing home sales / Case-Shiller
- Consumer confidence / sentiment (Michigan, Conference Board)
- Trade balance
- Durable goods orders
- Jobless claims (initial, continuing)
- ISM manufacturing / services

### Step 3: Fiscal & Regulatory Policy

Collect developments from:

- **US**: Congressional actions, executive orders, Treasury announcements, SEC/CFTC rulemakings, tax policy changes, debt ceiling/government funding status, tariff/trade actions
- **Europe**: EU regulatory actions, fiscal policy, ECB/EBA announcements, MiFID/AIFMD changes
- **UK**: FCA actions, budget/fiscal announcements, post-Brexit regulatory divergence
- **China**: State Council directives, CSRC actions, property market policy, tech regulation
- **Global**: G7/G20 statements, IMF/World Bank announcements, WTO rulings

For each: state what happened, when, and which sectors/assets are directly affected. No speculation on market reaction.

### Step 4: Geopolitical Events

Track confirmed developments in:

- **Active conflicts**: Military actions, ceasefire negotiations, humanitarian corridors, sanctions changes
- **Trade relations**: Tariff announcements, trade agreement progress, export controls, sanctions (new/lifted)
- **Energy security**: OPEC+ decisions, pipeline disruptions, LNG supply changes, strategic reserve actions
- **Elections & political transitions**: Election results, government formation, policy platform announcements with direct market implications
- **Supply chain**: Port disruptions, shipping route changes, semiconductor supply, critical mineral access
- **Cyber/tech**: Major cyber incidents affecting markets or infrastructure, AI regulation developments

For each: report only what has been confirmed by official sources or multiple credible news outlets. State the source. No speculation on escalation paths or outcomes.

### Step 5: Corporate & Deal Activity (Macro-Relevant)

- Major M&A announcements (>$1B deal value)
- Significant IPO pricings or filings
- Large corporate defaults or restructurings
- Major earnings surprises (mega-cap or sector bellwethers)
- CEO departures at major companies
- Significant activist campaigns launched
- Major credit rating changes (sovereign or large-cap corporate)

For each: company/entity, what happened, deal value if applicable, source.

### Step 6: Commodities & Energy Developments

- OPEC+ production decisions or compliance data
- US inventory data (EIA crude, products, natural gas)
- Weather events affecting supply (hurricanes, droughts, freezes)
- Mine/refinery outages or restarts
- Government policy on energy (subsidies, bans, mandates)
- Critical minerals supply chain developments

## Output Format

Organize into clearly labeled sections. Each item should be:

```
**[TIME ET] [HEADLINE]**
[1-2 sentence factual description]. Source: [source name].
```

- Order items by market relevance within each section
- Flag items with `[BREAKING]` only if occurred within the last 2 hours
- Flag items with `[UPDATED]` if a story has materially evolved during the day
- Include direct quotes for central bank language — do not paraphrase policy statements
- If a section has no developments, state "No significant developments" — do not omit the section

## Data Sources

Use MT Newswires MCP server as primary news source. Supplement with web search for geopolitical developments not covered by financial news feeds. Cross-reference with official government/central bank websites for policy actions.
