---
name: go
description: Smart dispatcher — describe what you need in plain English and get routed to the right command
tags:
  - dispatch
  - router
  - natural-language
  - smart
placeholder: "e.g. Analyze Fund III performance, geopolitical risks for our portfolio, public comps for healthcare portcos"
defaultOutput: Document
icon: IconPlayerPlay
arguments:
  - name: request
    description: Your request in natural language (e.g. "LP report for Fund IV", "geopolitical risk assessment", "find add-on targets")
    required: true
---

# /go — Smart Command Dispatcher

Route the user's natural-language request to the correct specialized command.

## User Request

**$ARGUMENTS**

## Routing Table

Classify the request against these intent patterns and route to the matching command:

### PE CFO — Core Analytics

| Intent Pattern | Command | Indicators |
|----------------|---------|------------|
| Research, analysis, deep-dive, investigate, explore a topic | `/research` | "analyze", "research", "deep-dive", "investigate", "what's driving", "explain why", "explore" |
| Fund metrics, IRR, TVPI, DPI, RVPI, PME, fund performance numbers | `/fund-metrics` | "IRR", "TVPI", "DPI", "RVPI", "PME", "compute metrics", "fund performance", "returns" |
| IC memo, investment memo, deal memo, exit memo | `/ic-memo` | "IC memo", "investment memo", "deal memo", "exit memo", "write memo for", "investment committee" |

### PE CFO — Portfolio Intelligence

| Intent Pattern | Command | Indicators |
|----------------|---------|------------|
| LP report, quarterly report, annual report, investor report, investor communication | `/lp-reporting` | "LP report", "quarterly report", "annual report", "investor update", "ILPA", "LP communication", "investor letter" |
| Portfolio monitoring, portfolio review, portco dashboard, KPI tracking, how companies are doing | `/portfolio-monitor` | "portfolio review", "portfolio monitor", "dashboard", "how are our companies", "KPI tracking", "portfolio snapshot", "underperformers", "outperformers" |
| Value creation, return attribution, value bridge, operational improvement tracking | `/value-creation` | "value creation", "value bridge", "return attribution", "margin expansion", "revenue growth", "operational improvement", "what's driving returns" |
| Public comps, comparable companies, trading multiples, stock performance of comps | `/public-comps` | "public comps", "comparables", "trading multiples", "stock performance", "comp set", "market comps", "public market", "key comps", "how are comps trading" |

### PE CFO — Risk & Geopolitical

| Intent Pattern | Command | Indicators |
|----------------|---------|------------|
| Geopolitical risk, macro risk, tariff impact, trade policy, sanctions, global risk | `/geopolitical-risk` | "geopolitical", "macro risk", "tariff", "trade policy", "sanctions", "global risk", "political risk", "interest rates", "inflation impact" |
| Geographic risk, election impact, zoning, local politics, state/country risk | `/geographic-risk` | "geographic risk", "election", "zoning", "local politics", "state risk", "country risk", "regulatory risk by geography", "jurisdiction" |
| Risk assessment, risk scoring, weighted risk matrix, risk/opportunity analysis | `/risk-assessment` | "risk assessment", "risk matrix", "risk scoring", "weighted risk", "risk/opportunity", "risk factors", "risk register" |

### PE CFO — Strategic

| Intent Pattern | Command | Indicators |
|----------------|---------|------------|
| Acquisition targets, add-on M&A, bolt-on, deal sourcing, investment targets | `/acquisition-targets` | "acquisition target", "add-on", "bolt-on", "M&A target", "deal sourcing", "buy-and-build", "find targets", "investment pipeline" |
| Action plan, priorities, what to do next, initiative ranking, execution plan | `/action-plan` | "action plan", "priorities", "what should we do", "next steps", "initiative ranking", "execution plan", "prioritize" |

### PE CFO — Existing Commands

| Intent Pattern | Command | Indicators |
|----------------|---------|------------|
| Portfolio company metrics, ILPA PortCo report, single-company PE analysis | `/portfolio-performance` | "ILPA", "PortCo", "portfolio company report", "portco metrics", "company KPIs" |
| Benchmark, peer comparison, quartile ranking, vintage comparison | `/benchmark` | "benchmark", "peer comparison", "quartile", "ranking", "compare to peers", "vintage" |
| Data room, parse documents, ingest files, index documents | `/data-room` | "data room", "parse", "ingest", "index documents", "uploaded files" |
| Demo, example, sample data, test run | `/example` | "example", "demo", "sample", "try", "test run" |
| Status, progress, where are we, what's done | `/status` | "status", "progress", "where are we", "what's done" |
| Rent roll, tenant roster, contracted income snapshot | `/rent-roll` | "rent roll", "tenant list", "contracted income", "lease roster" |

## Instructions

1. **Classify the request**: Read the user's request and match it against the routing table above. Look for keyword matches and semantic intent, not just exact phrases.

2. **If the intent is clear** (maps to exactly one command):
   - State which command you're routing to and why, in one short line (e.g., "Routing to `/geopolitical-risk` — you're asking about tariff exposure.")
   - Execute that command's full workflow immediately, passing the relevant portion of the request as the argument. Follow the target command's instructions exactly as if the user had invoked it directly.

3. **If the intent is ambiguous** (could map to multiple commands):
   - State which commands matched and why (e.g., "This matches `/risk-assessment` and `/geopolitical-risk` — running both.")
   - Execute all matching commands sequentially, passing the user's request to each one.
   - Clearly separate the output of each command with a heading so the user can distinguish results.

4. **If the request doesn't match any command**:
   - Tell the user their request doesn't map to a known workflow.
   - List the available commands grouped by category:

     **PE CFO — Core Analytics:**
     - `/research` — Deep-dive analysis on any PE/VC topic
     - `/fund-metrics` — Compute IRR, TVPI, DPI, and other fund metrics
     - `/ic-memo` — Investment committee memo for a deal

     **PE CFO — Portfolio Intelligence:**
     - `/lp-reporting` — Generate LP reports with fund performance and portfolio updates
     - `/portfolio-monitor` — Portfolio monitoring dashboard with KPI tracking
     - `/value-creation` — Value creation decomposition and forward planning
     - `/public-comps` — Public market comparables and valuation impact

     **PE CFO — Risk & Geopolitical:**
     - `/geopolitical-risk` — Geopolitical and macroeconomic risk assessment
     - `/geographic-risk` — Geographic and political risk by location
     - `/risk-assessment` — Weighted risk/opportunity scoring with action plans

     **PE CFO — Strategic:**
     - `/acquisition-targets` — Screen and evaluate M&A targets
     - `/action-plan` — Prioritized action plans with timing rationale

     **Portfolio & Reporting:**
     - `/rent-roll` — Rent roll and contracted income snapshot
     - `/benchmark` — Peer benchmarking and quartile analysis
     - `/data-room` — Parse and index a data room
     - `/example` — Demo with fabricated data

## Workspace Rules (MANDATORY)

Before executing any command, follow these rules:

1. **All files go in `output/`.** Run `mkdir -p output _research` first. Save every deliverable (PDF, DOCX, XLSX, PPTX, CSV, MD) to the `output/` subdirectory — e.g. `output/report.pdf`. The runtime ONLY collects files from `output/` — files written anywhere else will NOT be returned to the user.
2. **Use relative paths only.** Never write to `/home/user/`, `/home/agent/`, `/tmp/`, or any absolute path outside cwd.
3. **Don't waste turns on setup.** Do not check `$HOME`, do not explore the filesystem. Start working immediately.

## Design System (MANDATORY for file output)

When the routed command produces a file deliverable, read these design references BEFORE generating:

1. `/shared/plugins/accounting-c1a0cf4f/skills/design-system/references/tokens.md` — colors, typography, number formatting
2. `/shared/plugins/accounting-c1a0cf4f/skills/design-system/references/components.md` — title page, table, KPI card, chart patterns
3. `/shared/plugins/accounting-c1a0cf4f/skills/design-system/references/language.md` — PE/VC terminology, tone, disclaimers
4. `/shared/plugins/accounting-c1a0cf4f/brand/assets/brand-overrides.json` — firm name, confidentiality notice
5. Copy logo into workspace: `cp /shared/plugins/accounting-c1a0cf4f/brand/assets/logo.png ./logo.png 2>/dev/null || true`

## Critical Rules

- Always route — never answer the question yourself. The specialized commands have the domain logic.
- When the intent is clear, proceed immediately without asking for confirmation.
- When ambiguous, run all matching commands — don't ask, don't guess, just run them all.
- Pass the user's original request context through to the target command so nothing is lost.
