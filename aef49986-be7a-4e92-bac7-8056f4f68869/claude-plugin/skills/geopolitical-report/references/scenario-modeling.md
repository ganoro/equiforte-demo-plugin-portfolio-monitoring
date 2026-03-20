# Scenario Modeling Framework

## Standard Three-Scenario Model

| Scenario | Probability Range | Description |
|----------|------------------|-------------|
| **Base Case** | 50-65% | Current geopolitical trajectory with incremental evolution |
| **Stress Case** | 20-35% | Specific escalation that materially disrupts one or more risk dimensions |
| **Tail Risk** | 5-15% | Severe, low-probability event with systemic portfolio impact |

## Scenario Construction Rules

1. **Internal consistency** — if sanctions escalation is assumed, ALL companies with exposure must show impact
2. **Quantify in MOIC terms** — every scenario must produce a portfolio-level MOIC estimate
3. **Identify triggers** — observable events that signal scenario transition
4. **Time-bound** — every scenario has a time horizon (3-12 months)
5. **Actionable** — each scenario has associated hedging or mitigation actions

## MOIC Impact Estimation per Scenario

For each scenario x company:

```
Revenue_at_Risk = Affected_Revenue × Probability_of_Disruption × Severity_Factor
EBITDA_Impact = Revenue_at_Risk × Contribution_Margin
Value_Impact = EBITDA_Impact × Applicable_Multiple
New_Value = Current_Value - Value_Impact
Scenario_MOIC = (New_Value + Realized_Distributions) / Total_Invested
```

Where:
- **Severity_Factor**: 0.0 (no impact) to 1.0 (complete loss)
- **Probability_of_Disruption**: Scenario-specific probability
- **Contribution_Margin**: Incremental margin on affected revenue
- **Applicable_Multiple**: EV/EBITDA multiple for the sector

## Portfolio-Level Aggregation

```
Portfolio_MOIC_scenario = Sum(Company_Value_scenario × Ownership%) / Sum(Invested_Capital)
```

Present as a waterfall: Current MOIC → Risk adjustments → Opportunity adjustments → Scenario MOIC.
