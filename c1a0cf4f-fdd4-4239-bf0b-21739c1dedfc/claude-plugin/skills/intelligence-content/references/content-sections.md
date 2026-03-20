# Intelligence Content Section Guidelines

Detailed guidance for writing each section of each content type. All content uses HTML formatting within YAML `preview` and `full_content` fields.

## Daily Brief Sections

### 1. Market Snapshot

**Purpose:** Rates, spreads, deal activity at a glance. Lead section — always in preview.

**Format:** Use `<table>` with key indices. Include Close/Level, Change, and % Change columns.

**What to include:**
- Major equity indices (S&P 500, DJIA, Nasdaq, international)
- US Treasury yields (2Y, 10Y, 30Y) with bps changes
- Credit spreads (IG OAS, HY OAS, leveraged loan index)
- Key commodities (WTI, gold)
- DXY and major FX
- VIX

**Quality criteria:**
- All numbers sourced — never estimate
- Use `N/A` for unavailable data
- Positive: `+1.23`, Negative: `-1.23`, Unchanged: `Unchanged`
- Rate changes always in bps
- Keep to one concise table, not separate tables per asset class

### 2. Regulatory Watch

**Purpose:** New rules, comment periods, deadlines, and regulatory guidance affecting PE/credit funds.

**Research approach:** Search for SEC, CFTC, EU (AIFMD, SFDR), UK (FCA) regulatory actions. Focus on:
- Proposed/final rules affecting fund managers
- Comment period openings and deadlines
- Enforcement actions relevant to PE/credit
- Tax law changes (carried interest, SALT, international tax treaties)
- State-level regulatory changes (blue sky, ESG disclosure mandates)

**Format:** Each item as `<p><strong>Headline</strong> — Description with affected parties, dates, and required actions.</p>`

**Quality criteria:**
- Include specific deadlines and effective dates
- State which fund types/sizes are affected
- Actionable — what should a CFO do about this?
- 2-4 items per day. If no significant regulatory news, state "No significant regulatory developments today."

### 3. Operational Intel

**Purpose:** Fund administration, technology, vendor news, and operational developments PE CFOs need to know.

**Research approach:** Search for:
- Fund admin platform changes (Allvue, eFront, Burgiss, Investran, iLevel)
- PE tech M&A and product launches
- ILPA guideline updates, DDQ template changes
- Audit/accounting standard changes (ASC 820 fair value, GAAP/IFRS updates)
- Cybersecurity incidents affecting fund services
- Insurance market changes (D&O, cyber, E&O for fund managers)
- Outsourcing trends (NAV calculation, tax compliance, ESG reporting)

**Format:** Each item as `<p><strong>Headline</strong> — Description with timeline and impact.</p>`

**Quality criteria:**
- Focus on changes that require CFO action or awareness
- Include migration timelines for vendor changes
- 2-3 items per day

### 4. Data Snapshot

**Purpose:** Key metrics in a compact table. Quick reference for the most important numbers.

**Format:** Single `<table>` with Metric, Current, Change columns.

**What to include:**
- Fed Funds Rate
- Key credit spreads (IG OAS, HY OAS)
- Leveraged loan index level
- PE deal count (MTD or WTD if available)
- Any other headline number from the day

**Quality criteria:**
- Maximum 8-10 rows
- Numbers must match those in Market Snapshot section
- Use consistent formatting (bps for rates, $ for prices, % for returns)

### 5. The CFO Take

**Purpose:** 3 actionable items for PE CFOs to think about today. The editorial value-add.

**Format:**
```html
<p><strong>3 things PE CFOs should be thinking about today:</strong></p>
<ul>
  <li><strong>Topic</strong> — Actionable guidance in 1-2 sentences.</li>
  <li><strong>Topic</strong> — Actionable guidance in 1-2 sentences.</li>
  <li><strong>Topic</strong> — Actionable guidance in 1-2 sentences.</li>
</ul>
```

**Quality criteria:**
- Derived from the day's data and news — not generic advice
- Each item ties to something reported elsewhere in the brief
- Actionable: starts with what to do (review, coordinate, prepare, update, evaluate)
- PE CFO perspective: operations, compliance, LP relations, fund admin, treasury

### 6. Coming This Week

**Purpose:** Forward calendar of events and data releases for the rest of the week.

**Format:** `<ul>` with items grouped by day. Include time (ET) for economic releases.

**What to include:**
- Economic data releases (NFP, CPI, PMI, etc.)
- Central bank meetings/speeches
- Key earnings reports
- Conferences relevant to PE/credit
- Treasury auctions

**Quality criteria:**
- Only high-importance events
- Include day + time (ET)
- Cover remaining days of current week + key items for next week

---

## Private Markets Pulse Sections

### 1. Today's Priority Signals

**Purpose:** Categorized signals by urgency. The lead section.

**Format:** Use emoji indicators:
- 🔴 **Action Required** — items needing immediate CFO attention
- 🟡 **Monitor** — developments to watch, not yet actionable
- 🟢 **Opportunity** — potential advantages to explore

**Research approach:** Synthesize from market data, regulatory news, and deal activity. Prioritize by:
- Direct financial impact on fund operations
- Time sensitivity (deadlines, windows closing)
- Competitive advantage potential

**Quality criteria:**
- 1-2 items per category (3-6 total signals)
- Each signal in one paragraph: what happened + why it matters + what to do
- Derived from actual data/news, not hypothetical scenarios

### 2. Deep Dive

**Purpose:** In-depth analysis of one market theme. The most substantive section.

**Research approach:** Select the most significant theme from today's data. Search for:
- Supporting data points and historical context
- Market participant commentary
- Implications for PE/credit fund operations

**Format:** 3-5 paragraphs with subheadings:
```html
<h3>Deep Dive: [Theme]</h3>
<p>Opening with the core data point...</p>
<p><strong>What's driving it:</strong> Analysis of causes...</p>
<p><strong>CFO implication:</strong> What this means for fund operations...</p>
```

**Quality criteria:**
- Data-driven, not opinion-driven
- Include specific numbers and sources
- Clear CFO action items
- 300-500 words

### 3. LP/GP Signals

**Purpose:** Fundraising, LP allocation changes, secondary market activity, co-investment trends.

**Research approach:** Search for:
- Major LP allocation changes (pension funds, sovereign wealth, endowments)
- New fund launches and closes
- Co-investment vehicle announcements
- Secondary market pricing and volume
- LP advisory committee trends
- DPI demands and liquidity solutions (NAV lending, GP-led secondaries)

**Format:** `<ul>` with items, each as `<li><strong>LP/GP name</strong> — description.</li>`

**Quality criteria:**
- Name specific LPs and GPs when public
- Include deal sizes and pricing where available
- 3-5 items

### 4. Sector Spotlight

**Purpose:** Rotating analysis of PE/credit activity in a specific sector.

**Research approach:** Rotate through sectors: Healthcare, Technology, Financial Services, Industrials, Consumer, Energy/Infrastructure. Search for:
- Recent PE exits and entries in the sector
- Sector-specific multiples and trends
- Regulatory changes affecting the sector
- Platform vs. add-on deal activity

**Format:** Opening paragraph + data table if deals available:
```html
<h3>Sector Spotlight: [Sector]</h3>
<p><strong>Theme</strong> — Summary of sector activity...</p>
<table>
  <tr><th>Company</th><th>Sponsor</th><th>Type</th><th>EV</th><th>Multiple</th></tr>
  ...
</table>
```

**Quality criteria:**
- Rotate sectors across days
- Include specific deal data when available
- 150-300 words

---

## Preview vs. Full Content Split

For all article types, the `preview` field contains the first 2-3 sections, and `full_content` contains ALL sections. The preview MUST be a subset of the full content.

### Daily Brief Split
- **Preview (ungated):** Market Snapshot + Regulatory Watch
- **Full Content (gated):** All 6 sections

### Pulse Split
- **Preview (ungated):** Today's Priority Signals + Deep Dive opening
- **Full Content (gated):** All 4 sections

### CFO Insights Split
- **Preview (ungated):** Survey Highlights
- **Full Content (gated):** All 4 sections
