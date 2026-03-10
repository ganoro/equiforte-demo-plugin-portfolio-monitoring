---
name: action-plan
description: Generate prioritized action plans with timing rationale, resource requirements, and success metrics for portfolio or fund-level initiatives
tags:
  - action-plan
  - priorities
  - execution
  - timeline
  - initiatives
placeholder: "e.g. Action plan for Fund III portfolio optimization, or Prioritize initiatives for Acme Corp value creation"
defaultOutput: Document
icon: IconChecklist
arguments:
  - name: scope
    description: "Fund, portfolio company, or topic for action planning"
    required: true
  - name: constraints
    description: "Constraints to apply (comma-separated). e.g. 'budget $2M, team capacity 3 FTE, must complete before Q4'"
    required: false
---

# /action-plan — Prioritized Action Plan

Generate a prioritized, time-bound action plan with explicit timing rationale and resource requirements.

## Parameters

- **Scope**: $ARGUMENTS
- **Constraints**: (from arguments, if provided)

## Efficiency Rules (TARGET: 600 seconds)

- Draw from existing workspace analysis — don't re-research from scratch
- If no prior analysis exists, run a quick assessment first (5-8 web searches max)
- Focus on the top 15-20 actions, not an exhaustive list
- One consolidated plan, not separate plans per category

## Instructions

### Step 1 — Gather Context

Review workspace for:
- Prior risk assessments, portfolio reviews, value creation analyses
- Known issues, data gaps, and flagged items
- Fund strategy and LP commitments
- Resource constraints and timelines

### Step 2 — Identify Actions

Categorize actions:

**Portfolio Operations:**
- Revenue acceleration initiatives
- Cost optimization programs
- Management team changes
- Technology/digital transformation
- Add-on acquisition execution

**Fund Management:**
- LP communication and reporting
- Capital deployment planning
- Exit preparation and timing
- Co-investment opportunities
- Fund-level risk mitigation

**Strategic:**
- Market positioning adjustments
- Competitive response actions
- Regulatory compliance initiatives
- ESG implementation

### Step 3 — Prioritize Using ICE Framework

Score each action on:
- **Impact** (1-10): Magnitude of expected outcome
- **Confidence** (1-10): How certain we are this will work
- **Ease** (1-10): Inverse of effort/complexity/cost

**Priority Score** = Impact × Confidence × Ease / 10

| # | Action | Category | Impact | Confidence | Ease | Priority Score | Timing |
|---|--------|----------|--------|-----------|------|---------------|--------|

### Step 4 — Timing Classification with Rationale (use `action-prioritization` skill)

For each action, assign timing with explicit reasoning:

| Action | Timing | Rationale | Dependencies | Risks of Delay |
|--------|--------|-----------|-------------|----------------|

**Timing Logic:**
- **Immediate** (0-30 days): Why can't this wait? What deteriorates if we delay?
- **Short-Term** (1-3 months): What needs to happen first? Why not immediate?
- **Medium-Term** (3-12 months): What external factors determine timing? What's the setup work?
- **Long-Term** (12+ months): What market conditions or milestones trigger this?

### Step 5 — Resource Requirements

| Action | Team/Skill Required | Estimated Hours | External Cost | Internal Capacity Available? |
|--------|--------------------|-----------------|--------------|-----------------------------|

Flag resource conflicts where multiple high-priority actions compete for the same resources.

### Step 6 — Success Metrics & Checkpoints

| Action | Success Metric | Baseline | Target | Checkpoint Date | Escalation Trigger |
|--------|---------------|----------|--------|-----------------|-------------------|

### Step 7 — Execution Timeline

Present a Gantt-style timeline (text-based):

```
Q1 2026:  [████ Action A ████] [██ Action B ██]
Q2 2026:  [████████ Action C ████████] [██ Action D ██]
Q3 2026:  [██ Action E ██] [████ Action F ████]
```

### Step 8 — Generate Output

Save to `output/action-plan-[scope]-[date].docx`.
Offer XLSX with full scoring and timeline data.
Offer PPTX for board/IC presentation.

## Critical Rules

- Every timing classification must have an explicit rationale
- Don't create 50 actions — focus on the vital 15-20
- Resource requirements must be realistic, not aspirational
- Success metrics must be measurable, not vague
- Flag dependencies between actions
- Include "do nothing" risk for each action to justify prioritization
- Constraints from user must be respected (budget, timeline, capacity)

## Workspace Rules (MANDATORY)

1. Run `mkdir -p output _research` first
2. All deliverables to `output/` only
3. Use relative paths only
