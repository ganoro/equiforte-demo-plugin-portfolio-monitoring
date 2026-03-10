---
description: >
  Geographic and political risk assessment framework for PE portfolio companies. Triggers on:
  "geographic risk", "political risk", "election risk", "zoning risk", "regulatory risk",
  "local risk", "jurisdiction risk", "country risk", "state risk", "geographic exposure",
  "election impact", "policy risk". Provides methodology for mapping, scoring, and mitigating
  location-specific risks across a PE portfolio.
---

# Geographic Risk — Location-Specific Risk Assessment

## Purpose

Map and assess geographic, political, and regulatory risks that may impact PE portfolio companies based on their physical locations, revenue geography, supply chains, and regulatory jurisdictions.

## Risk Categories

### 1. Political Risk

| Factor | Assessment Approach |
|--------|-------------------|
| Election cycles | Identify upcoming elections at federal, state, local level. Model policy impact for each likely outcome. Never predict winners. |
| Policy direction | Assess current administration's trajectory on key issues (tax, regulation, trade, labor) |
| Political stability | EIU Political Stability Index, historical precedent, institutional strength |
| Lobbying/influence | Portco's ability to shape policy vs. passive exposure |

### 2. Regulatory Risk

| Factor | Assessment Approach |
|--------|-------------------|
| Enacted regulation | Already law — assess compliance cost and timeline |
| Proposed regulation | In legislative process — assess probability and impact |
| Speculative regulation | Discussed but not proposed — monitor, don't overweight |
| Zoning & permitting | Local government land use decisions — assess specific municipal context |
| Environmental regulation | EPA, state-level, ESG mandates |
| Labor regulation | Minimum wage, unionization rules, employment law changes |
| Data privacy | GDPR, CCPA, state-level privacy laws |
| Industry-specific | Healthcare (CMS), financial services (SEC/FINRA), defense (ITAR/EAR) |

### 3. Economic Risk

| Factor | Data Source |
|--------|------------|
| GDP growth | BEA (federal), state economic agencies |
| Unemployment rate | BLS |
| Wage growth | BLS, ADP data |
| Cost of living trend | BLS CPI by metro area |
| Population growth/decline | Census Bureau |
| Business climate | State rankings (CNBC, Tax Foundation, etc.) |
| Infrastructure quality | ASCE report card |

### 4. Geographic Concentration

Flag portfolio companies with concentrated geographic exposure:

| Concentration Level | Threshold | Action |
|--------------------|-----------| -------|
| Critical | >50% revenue or operations in single jurisdiction | Immediate assessment, diversification plan |
| High | 25-50% | Detailed risk analysis, monitoring |
| Moderate | 10-25% | Standard monitoring |
| Low | <10% | Acceptable — periodic review |

## Scoring Methodology

Use the `risk-weighting` skill scoring framework applied to geographic factors:

- **Probability**: Likelihood of the geographic risk materializing (1-10)
- **Severity**: Impact on the affected portco's value (1-10)
- **Exposure Factor**: Portfolio NAV exposed to this geographic risk (0.1-1.0)

**Geographic Risk Score** = Probability × Severity × Exposure Factor

## Scenario Modeling

For material election/policy risks, model scenarios:

**Scenario A** (Outcome 1): Policy implications, portco impact, probability assessment
**Scenario B** (Outcome 2): Policy implications, portco impact, probability assessment

For each scenario, estimate:
- Revenue impact (% change)
- Cost/margin impact (bps change)
- Valuation multiple impact
- Timeline of impact (immediate vs. phased)

## Source Requirements

| Source Type | Quality Tier | Usage |
|-------------|-------------|-------|
| Government data (BLS, Census, BEA) | Tier 1 | Economic fundamentals |
| EIU, Oxford Economics | Tier 1 | Country/political risk ratings |
| Goldman, JP Morgan research | Tier 2 | Policy impact analysis |
| State/local government publications | Tier 2 | Regulatory pipeline |
| News sources (Reuters, Bloomberg, FT) | Tier 3 | Current events, breaking policy |

Always cite source with date. Flag when relying on AI inference vs. published analysis.

## Critical Rules

1. Never predict election outcomes — model scenarios for each plausible outcome
2. Distinguish enacted vs. proposed vs. speculative regulatory changes
3. Don't overweight tail risks — probability-weight all assessments
4. Include historical precedent: "When [similar policy] was enacted in [year], the impact was [X]"
5. Update assessment when material events occur (elections, policy announcements)
6. Flag immediately if any portco has sanctions exposure
