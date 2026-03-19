---
name: event-calendar
description: Compile upcoming financial events, economic releases, earnings, conferences, central bank meetings, and deal milestones. Use when generating a daily brief or when the user asks about upcoming events, the economic calendar, or conference schedules.
---

# Event Calendar

Compile a forward-looking calendar of scheduled events relevant to financial professionals. Cover the current week plus the next two weeks. All dates and times in Eastern Time (ET) unless otherwise noted.

## Data Collection Workflow

### Step 1: Economic Calendar (Next 2 Weeks)

Gather all scheduled releases with:

| Field | Description |
|---|---|
| Date | Release date |
| Time (ET) | Scheduled time |
| Country | Issuing country |
| Indicator | Official name |
| Period | Reference period |
| Prior | Previous reading |
| Consensus | Market consensus (if available) |
| Importance | High / Medium / Low |

**High-importance releases to always include:**
- US: NFP, CPI, PPI, PCE, GDP, FOMC decision, retail sales, ISM, jobless claims
- Europe: ECB decision, Eurozone CPI, GDP, PMIs
- UK: BoE decision, CPI, GDP, PMIs
- China: PBoC decision, GDP, CPI, PMIs, trade balance
- Japan: BoJ decision, CPI, GDP, Tankan
- Global: G7/G20 summits, IMF meetings

### Step 2: Central Bank Calendar

For each major central bank, list:

| Bank | Next Meeting | Rate Decision Expected | Minutes/Statement Due |
|---|---|---|---|

Track:
- FOMC (Fed)
- ECB Governing Council
- BoE MPC
- BoJ Policy Board
- PBoC
- RBA
- Bank of Canada
- SNB
- Riksbank
- Norges Bank

Also note:
- Scheduled speeches by governors/chairs/board members (with topic if known)
- Blackout periods (when officials cannot speak publicly before meetings)
- Quantitative tightening / balance sheet runoff dates

### Step 3: Earnings Calendar

**This Week:**
List all companies reporting, organized by date and time (before market / after market):

| Date | Time | Company | Ticker | Sector | Consensus EPS | Consensus Revenue |
|---|---|---|---|---|---|---|

**Next Week:**
Same format, with emphasis on:
- S&P 500 constituents
- Sector bellwethers
- Companies relevant to active deal pipelines (PE, IB)
- Names with high short interest or recent activist activity

**Earnings Season Stats (if in earnings season):**
- % of S&P 500 reported
- % beating EPS estimates
- % beating revenue estimates
- Blended earnings growth rate (vs. year-ago)
- Blended revenue growth rate

### Step 4: Conferences & Industry Events

Gather conferences and industry events for the next 4 weeks:

| Date(s) | Event | Location | Host/Organizer | Key Sectors | Notable Presenters |
|---|---|---|---|---|---|

**Categories to cover:**
- **Investor conferences**: Goldman Sachs, JPMorgan, Morgan Stanley, Barclays, UBS, Citi, BofA, Jefferies, Piper Sandler, RBC, etc.
- **Industry conferences**: CES, HIMSS, NRF, RSA, MWC, CERAWEEK, etc.
- **PE/VC events**: SuperReturn, PEI events, ACG conferences, ILPA events
- **Credit/debt events**: Leveraged Finance conferences, CLO/ABS summits, private credit events
- **Hedge fund events**: SALT, Sohn, Ira Sohn, Delivering Alpha
- **Central bank symposia**: Jackson Hole, Sintra ECB Forum, BoE events
- **Regulatory**: SEC open meetings, Congressional hearings on financial topics

For each event, note if company presentations are scheduled that may contain material non-public forward guidance.

### Step 5: IPO & Capital Markets Calendar

**IPO Pipeline:**
| Company | Ticker | Exchange | Expected Date | Deal Size | Lead Bookrunners | Sector |
|---|---|---|---|---|---|---|

**Secondary Offerings / Block Trades:**
- Notable follow-on offerings filed or expected

**Debt Issuance Calendar:**
- US Treasury auction schedule (bills, notes, bonds, TIPS)
- Major investment-grade corporate issuance expected
- High-yield / leveraged loan pricings expected
- Sovereign issuance (major economies)

### Step 6: Regulatory & Legal Deadlines

- SEC filing deadlines (10-K, 10-Q, proxy season dates)
- Antitrust review deadlines for pending mergers
- Major court rulings expected (antitrust, patent, regulatory challenges)
- Regulatory comment period closings
- Index rebalancing dates (S&P 500, Russell, MSCI)
- Options/futures expiration dates (monthly, quarterly)
- Tax deadlines

### Step 7: Deal Milestones (if focus is PE, IB, or PD)

- Expected deal closings (large M&A)
- Shareholder vote dates for pending transactions
- Go-shop period expirations
- Tender offer deadlines
- SPAC redemption/extension deadlines
- Notable fund closings / fundraise deadlines

## Output Format

Organize into a day-by-day calendar for this week, then a weekly summary for the following two weeks.

**Daily view (this week):**
```
### [Day, Date]

**Economic Releases**
- [Time ET] [Country] [Indicator] ([Period]) — Prior: [X], Consensus: [Y]

**Earnings**
- [BMO/AMC] [Company] ([Ticker]) — EPS est: $X.XX, Rev est: $X.XB

**Events**
- [Event name] ([Location]) — [Key details]

**Other**
- [Item]
```

**Weekly view (next 2 weeks):**
Group by category with dates noted.

- If a date/time is tentative, mark as `[TBD]`
- If consensus is not yet available, mark as `N/A`
- Never fabricate event dates or consensus estimates — use `N/A` if not found

## Data Sources

Use MCP servers (FactSet, Morningstar, S&P Global, MT Newswires, PitchBook) for earnings calendars, economic releases, and deal pipelines. Use web search for conference schedules, IPO calendars, and regulatory deadlines. Cross-reference dates with official sources (Treasury.gov, SEC EDGAR, exchange websites).
