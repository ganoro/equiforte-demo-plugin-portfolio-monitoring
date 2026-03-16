---
name: plugin-developer
description: Guide for creating or modifying plugin components — skills, commands, hooks, and agents
tags:
  - plugin
  - developer
  - skill
  - command
  - hook
  - agent
placeholder: "e.g. Create a command for quarterly LP reporting"
defaultOutput: Document
icon: IconCode
arguments:
  - name: request
    description: What you want to build (e.g. "new skill for X", "add a hook that validates Y", "create a command for Z")
    required: true
---

# /plugin-developer — Build Plugin Components

Create or modify skills, commands, hooks, agents, and automations for this plugin.

## User Request

**$ARGUMENTS**

## Component Types

| Component | What it does | Where it lives |
|-----------|-------------|----------------|
| **Command (Control)** | User-facing slash command with structured workflow (also called a "control") | `commands/<name>.md` |
| **Skill** | Teaches Claude how to do something — reference docs, formulas, workflows | `skills/<name>/SKILL.md` |
| **Hook** | Auto-runs on tool events — validation, quality checks, guardrails | `hooks/hooks.json` |
| **Agent** | Autonomous subagent with specific tools and role | `agents/<name>.md` |

---

## Creating a Command

Commands are the primary user-facing entry points. They MUST have:
1. **YAML frontmatter** with name, description, tags, placeholder, defaultOutput, icon, arguments
2. **A title** in the format `# /<command-name> — Descriptive Title`
3. **A user request section** that references `$ARGUMENTS`
4. **Numbered, detailed step-by-step instructions** — each step describes what to do, what data to extract, and how to present it
5. **Tables** showing expected output formats with column headers
6. **A Critical Rules section** with domain-specific validation rules

### QUALITY STANDARD — What a production command looks like

Below is a REAL command from this plugin. Study the depth, structure, and level of detail. Your output MUST match this quality:

```markdown
---
name: rent-roll
description: Generate a comprehensive rent roll — the core monthly snapshot of all contracted income across the property
tags:
  - real-estate
  - cre
  - rent-roll
  - tenant
  - lease
  - income
placeholder: "e.g. Generate rent roll for 100 Main Street as of March 2024"
defaultOutput: Spreadsheet
icon: IconBuilding
arguments:
  - name: property
    description: "Property name or address, or 'all' for full portfolio (default: current workspace property)"
    required: false
---

# /rent-roll — Rent Roll Report

Generate the most important recurring CRE report: a complete snapshot of contracted income for a property.

## Target

**$ARGUMENTS** (default: current workspace property)

## Instructions

### Step 1 — Gather Lease Data

Scan the workspace for lease agreements, rent schedules, and tenant records. Use the `document-parser` skill for PDFs/XLSX. Extract every active lease with full provenance.

### Step 2 — Build the Rent Roll Table

Produce a table with one row per tenant/suite:

| # | Tenant | Suite | GLA (SF) | Lease Start | Lease End | Base Rent (Annual) | Rent/SF | Escalation Schedule | CAM Structure | Security Deposit | Options/Renewals |
|---|--------|-------|----------|-------------|-----------|-------------------|---------|---------------------|---------------|-----------------|-----------------|

### Step 3 — Summarize Key Metrics

Below the table, present:

- **Total Contracted Base Rent** (annual and monthly)
- **Weighted Average Rent/SF** (weighted by GLA)
- **Weighted Average Lease Term (WALT)** remaining
- **Vacancy Rate** (% of GLA)
- **Expiring within 12 months** (% of GLA, % of rent)
- **CAM Structure Breakdown** (NNN vs. modified gross vs. gross — count and % of GLA)

### Step 4 — Escalation Schedule

Show upcoming rent escalations for the next 12 months:

| Tenant | Suite | Escalation Date | Current Rent/SF | New Rent/SF | Increase (%) | Annual Impact ($) |
|--------|-------|-----------------|-----------------|-------------|-------------- |-------------------|

### Step 5 — Flag Issues

Identify and flag:
- Leases expiring within 6 months with no renewal option
- Below-market rents (compare to market rent if available)
- Tenants with outstanding security deposit issues
- Missing or incomplete lease data (record as gaps)

### Step 6 — Write Output

Save the rent roll and update entity maps with tenant entities.

## Critical Rules

- Every rent figure must state: annual vs. monthly, gross vs. net, currency
- Every metric must have an as-of date
- Escalation schedules must be mathematically consistent (base × escalation % = new rent)
- Vacancy must reconcile: Occupied SF + Vacant SF = Total GLA
- Never fabricate data — mark missing fields as gaps
- Label confidence levels on all extracted values
```

### BAD vs GOOD command output

**BAD** (what NOT to produce — no frontmatter, no steps, no structure):
```
Gross Potential Rental Income
+ Other Income
= GPI
− Vacancy & Credit Loss
= EGI
− OpEx (taxes, insurance, mgmt, R&M, utilities, HOA, reserves)
= NOI
```

**GOOD** — A command must be a complete workflow guide with YAML frontmatter, multiple detailed steps, output tables, and critical rules. See the rent-roll example above.

### Command checklist

- [ ] YAML frontmatter with ALL fields (name, description, tags, placeholder, defaultOutput, icon, arguments)
- [ ] Title: `# /<name> — Descriptive Title`
- [ ] User request section with `$ARGUMENTS`
- [ ] At least 4-6 numbered steps with specific instructions
- [ ] At least one table showing expected output format
- [ ] Critical Rules section with domain-specific validation
- [ ] References to relevant skills where appropriate (e.g. "use the `document-parser` skill")
- [ ] File writing instructions if applicable

---

## Creating a Skill

For comprehensive guidance on writing skills, **read the `skill-creator` skill** at `skills/skill-creator/SKILL.md`. It covers the full skill-writing workflow including:

- Skill anatomy: YAML frontmatter, progressive disclosure, bundled resources
- Writing patterns: output formats, examples, writing style
- Description optimization for better triggering accuracy
- Directory structure and file organization

**Before writing a skill, read `skills/skill-creator/SKILL.md`** — specifically the "Writing the SKILL.md" and "Skill Writing Guide" sections. Follow its patterns for frontmatter, progressive disclosure, and description quality.

### Quick reference — Skill structure

```
skills/<skill-name>/
├── SKILL.md              # Main skill file (required)
├── scripts/              # Python/JS utilities (optional)
├── references/           # Supporting docs (optional)
└── assets/               # Templates, HTML, images (optional)
```

### Skill checklist

- [ ] YAML frontmatter with detailed `description` (determines when skill triggers — be specific and slightly "pushy" per skill-creator guidance)
- [ ] Clear title and purpose statement
- [ ] Detailed methodology with formulas, code, or step-by-step procedures
- [ ] Output tables or templates showing expected presentation format
- [ ] Critical rules or common pitfalls section
- [ ] Keep SKILL.md under 500 lines — put supporting details in `references/` files
- [ ] Include scripts for repeatable operations if applicable

---

## Creating a Hook

Hooks live in `hooks/hooks.json` and run automatically on events. They are also called "automations."

### hooks.json format

The file must contain a JSON object with a `hooks` array:

```json
{
  "hooks": [
    {
      "event": "PreToolUse",
      "tools": ["Write", "Edit"],
      "type": "prompt",
      "prompt": "Detailed prompt describing what to check and how to respond"
    }
  ]
}
```

### QUALITY STANDARD — What production hooks look like

```json
{
  "hooks": [
    {
      "event": "PreToolUse",
      "tools": ["Write", "Edit"],
      "type": "prompt",
      "prompt": "You are a PE/VC financial report quality checker. Review the content about to be written or edited. Check for these issues and warn (do not block) if any are found:\n\n1. Financial figures without an as-of date\n2. Monetary values without currency labels (USD, EUR, GBP, etc.)\n3. Return figures (IRR, returns) without gross/net designation\n4. Performance metrics without confidence level (VERIFIED/REPORTED/ESTIMATED/ASSUMED)\n5. Percentage values that seem unreasonable (IRR > 100% or < -50%, TVPI > 10x)\n\nIf writing to a file in _research/ or containing financial data, check these. For non-financial files, skip checks.\n\nRespond with a brief warning if issues found, or approve if clean."
    },
    {
      "event": "PostToolUse",
      "tools": ["Bash"],
      "type": "prompt",
      "prompt": "You are a computation sanity checker. If the bash command just executed was a Python script performing financial calculations, review the output for:\n\n1. TVPI should approximately equal DPI + RVPI (within rounding)\n2. IRR should be in a reasonable range (-50% to +100%)\n3. DPI and RVPI should be non-negative\n4. Percentages should sum correctly where applicable\n\nIf the command was not a financial calculation, skip checks.\n\nRespond with a brief sanity check result or flag any anomalies."
    },
    {
      "event": "Stop",
      "type": "prompt",
      "prompt": "You are a research completeness checker. Before the session ends, verify:\n\n1. All expected output files have been created\n2. Critical data gaps have been addressed or acknowledged\n3. A final output file exists\n\nDo not block — just inform. Respond with a brief completeness summary."
    }
  ]
}
```

### Available events

| Event | When it fires | Use for |
|-------|--------------|---------|
| `PreToolUse` | Before a tool runs | Validate inputs, block dangerous operations, check quality |
| `PostToolUse` | After a tool runs | Validate outputs, check computation results, verify provenance |
| `Stop` | When the agent finishes | Completeness checks, missing deliverables, gap summary |

### Hook checklist

- [ ] Each hook has a specific, focused concern (not a catch-all)
- [ ] Prompt describes the role (e.g. "You are a financial data quality checker")
- [ ] Prompt lists numbered criteria to check
- [ ] Prompt specifies when to skip (e.g. "For non-financial files, skip checks")
- [ ] Prompt specifies how to respond (warn, not block; brief summary)
- [ ] `tools` array scopes the hook to relevant tools only
- [ ] When modifying hooks.json, READ the existing file first to avoid overwriting other hooks

---

## Creating an Agent

Agents are autonomous subagents with specific tools and responsibilities. They MUST have:
1. **YAML frontmatter** with name, description, and tools list
2. **A role statement** ("You are a...")
3. **Numbered responsibilities**
4. **Operating rules** with specific constraints

### QUALITY STANDARD — What a production agent looks like

```markdown
---
name: data-aggregator
description: "Parallel data collection agent — parses documents, extracts structured facts, builds entity maps, and identifies data gaps. Handles PDF, XLSX, DOCX, and CSV files."
tools:
  - Bash
  - Read
  - Write
  - Edit
  - Glob
  - Grep
---

# Data Aggregator Agent

You are a data aggregation specialist. Your job is to collect, parse, and structure all available data in the workspace.

## Your Responsibilities

1. **Discover** all data files in the workspace (PDF, XLSX, DOCX, CSV, PPTX)
2. **Parse** each file using appropriate Python libraries (pdfplumber, openpyxl, python-docx, pandas)
3. **Extract** structured facts with full provenance:
   - Source document name and page/sheet/section
   - As-of date
   - Confidence level (VERIFIED / REPORTED / ESTIMATED / ASSUMED)
4. **Build entity map** — identify all entities and their relationships
5. **Identify gaps** — what data is missing, what would strengthen the analysis
6. **Write outputs** to structured files

## Operating Rules

- Process documents in priority order: financial statements → reports → legal → other
- Never fabricate data — if extraction fails or is ambiguous, flag it as a gap
- Tag every extracted fact with its provenance
- For scanned PDFs or image-based documents, note them as requiring OCR
- Cross-reference data across documents to verify consistency
```

### Agent checklist

- [ ] YAML frontmatter with name, detailed description, and tools list
- [ ] Title: `# <Agent Name> Agent`
- [ ] Role statement: "You are a <role>. Your job is to <responsibility>."
- [ ] Numbered responsibilities (5-7 specific tasks)
- [ ] Operating rules with constraints and priorities
- [ ] Specify output locations and formats

---

## Workspace Rules (MANDATORY)

1. **All created/modified files MUST be copied to `output/`.** Run `mkdir -p output` first. After writing any plugin file (command, skill, hook, agent), copy it to `output/` preserving the relative path. For example:
   - `commands/weekly-report.md` → `cp commands/weekly-report.md output/commands/weekly-report.md`
   - `skills/data-parser/SKILL.md` → `cp -r skills/data-parser output/skills/data-parser`
   - `hooks/hooks.json` → `cp hooks/hooks.json output/hooks/hooks.json`
   - `agents/reviewer.md` → `cp agents/reviewer.md output/agents/reviewer.md`
   The runtime ONLY collects files from `output/` — files written anywhere else will NOT be returned.
2. **Use `mkdir -p`** to create subdirectories inside `output/` before copying (e.g. `mkdir -p output/commands output/skills/my-skill`).
3. **Use relative paths only.** Never write to absolute paths outside cwd.

---

## Instructions

1. **Identify the component type** from the user's request. If unclear, ask.
2. **Read existing files** in the relevant directory to understand current plugin structure and avoid conflicts.
3. **Create the component** following the quality standards and checklists above. Every component must be production-quality — fully structured, with proper frontmatter, detailed instructions, tables, and rules.
4. **For commands**: Include 4-6 numbered steps, output tables, and critical rules. Never produce a command that is just plain text or a formula.
5. **For skills**: Include methodology, formulas or code, presentation templates, and pitfalls.
6. **For hooks**: Read existing `hooks/hooks.json` first, then add new hooks without overwriting existing ones.
7. **For agents**: Define clear role, responsibilities, tools, and operating constraints.
8. **Copy all created/modified files to `output/`** preserving relative paths (see Workspace Rules above).
9. **After creating**, confirm what was built and where it lives.

## Common Mistakes to Avoid

- **Creating a command that's just a formula or plain text** — commands must be complete workflow guides
- **Missing YAML frontmatter** — every command and agent MUST have it
- **Vague skill descriptions** — the description determines when the skill triggers; be specific
- **Overwriting hooks.json** — always merge with existing hooks
- **Generic instructions** like "Step 1, Step 2, Step 3" — each step must have specific, actionable detail
- **Forgetting to copy files to `output/`** — the runtime only returns files from `output/`
