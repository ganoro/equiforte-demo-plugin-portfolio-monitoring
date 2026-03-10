---
description: >
  Weighted risk and opportunity scoring framework for PE portfolio analysis. Triggers on:
  "risk assessment", "risk scoring", "weighted risk", "risk matrix", "opportunity assessment",
  "risk/opportunity", "risk weighting", "score risks", "risk factors". Provides the methodology
  for scoring, weighting, and ranking risks and opportunities across PE portfolios.
---

# Risk Weighting — PE Portfolio Risk & Opportunity Scoring

## Purpose

Provide a structured, adjustable framework for scoring and ranking risks and opportunities across a PE portfolio. All scores are transparent, adjustable by the user, and tied to specific portfolio impact.

## Scoring Methodology

### Individual Risk/Opportunity Score

Each factor is scored on three dimensions:

| Dimension | Scale | Description |
|-----------|-------|-------------|
| **Probability** | 1-10 | Likelihood of occurrence within the assessment horizon |
| **Impact** | 1-10 | Magnitude of effect on portfolio value if it occurs |
| **Exposure Factor** | 0.1-1.0 | Proportion of portfolio NAV exposed to this factor |

**Raw Score** = Probability × Impact × Exposure Factor

Maximum possible score: 100 (10 × 10 × 1.0)

### Category Weighting

Risks are grouped into categories, each with a weight (default weights below, adjustable):

| Category | Default Weight | Adjustable |
|----------|---------------|------------|
| Market & Competitive | 25% | Yes — user can override |
| Operational | 25% | Yes |
| Financial | 25% | Yes |
| Regulatory & Political | 15% | Yes |
| Strategic & Exit | 10% | Yes |

**Weighted Score** = Raw Score × (Category Weight / 25)

This normalizes so a factor in a 25%-weighted category scores at face value.

### Scoring Guidelines

**Probability Scale:**

| Score | Label | Meaning |
|-------|-------|---------|
| 1-2 | Very Low | Rare event, <10% chance in 12 months |
| 3-4 | Low | Unlikely but plausible, 10-30% chance |
| 5-6 | Medium | Reasonable possibility, 30-60% chance |
| 7-8 | High | More likely than not, 60-85% chance |
| 9-10 | Very High | Near-certain, >85% chance |

**Impact Scale:**

| Score | Label | Meaning |
|-------|-------|---------|
| 1-2 | Minimal | <2% NAV impact, no strategic change needed |
| 3-4 | Low | 2-5% NAV impact, minor operational adjustment |
| 5-6 | Moderate | 5-10% NAV impact, meaningful operational response |
| 7-8 | High | 10-20% NAV impact, strategic response required |
| 9-10 | Severe | >20% NAV impact, existential threat or transformative opportunity |

### Adjustability Protocol

When the user requests adjustments:

1. **Add a factor**: Insert into the matrix, score using the same methodology, re-rank all factors
2. **Change category weights**: Update weights (must sum to 100%), recalculate all weighted scores, re-rank
3. **Override a score**: Accept user's probability/impact/exposure override, recalculate weighted score, re-rank
4. **Add custom factors**: If the user identifies a risk the AI didn't surface, add it immediately and note "User-identified"
5. **Set thresholds**: Filter display to only show factors above a user-specified weighted score

Always confirm the adjustment and show before/after rankings for the top 10 factors.

### Risk Classification

| Weighted Score | Classification | Action Required |
|----------------|---------------|-----------------|
| ≥ 60 | Critical | Immediate action — executive attention |
| 40-59 | High | Short-term action plan (1-3 months) |
| 20-39 | Medium | Monitor and manage operationally |
| 10-19 | Low | Accept and monitor quarterly |
| < 10 | Minimal | Accept — no dedicated action |

### Trend Indicators

Track direction of each factor over time:

| Symbol | Meaning |
|--------|---------|
| ↑ | Increasing risk / improving opportunity |
| → | Stable |
| ↓ | Decreasing risk / diminishing opportunity |

### Historical Context

When scoring risks, cite historical precedent:
- "In [year], a similar [event] resulted in [X]% impact on comparable portfolios"
- Source attribution required (firm, report, date)
- Note when AI assessment relies on historical patterns vs. current intelligence

### Output Format

Present as a ranked table:

| Rank | Factor | Type | Category | Prob | Impact | Exposure | Raw Score | Cat Weight | Weighted Score | Trend | Horizon |
|------|--------|------|----------|------|--------|----------|-----------|-----------|---------------|-------|---------|

Follow with:
- Top 5 risks summary with mitigation recommendations
- Top 5 opportunities summary with capture actions
- Category-level aggregate scores
- Changes from prior assessment (if available)
