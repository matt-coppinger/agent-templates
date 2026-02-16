# Materiality Thresholds

Guidance on what constitutes a material variance requiring management attention.

## Threshold Framework

A variance is **material** if it breaches EITHER the percentage threshold OR the absolute threshold — whichever is hit first.

### Default Thresholds (from config.yaml)

| Line Item Type | % Threshold | Absolute Threshold |
|---------------|-------------|-------------------|
| Revenue | 5% | £50,000 |
| Cost items | 10% | £25,000 |
| All others | 10% | £10,000 |

### RAG Status Assignment

| Status | Condition | Action Required |
|--------|-----------|-----------------|
| 🟢 Green | Variance ≤ 5% of budget | No action — within acceptable tolerance |
| 🟡 Amber | Variance 5–15% of budget | Investigate — explain in commentary, monitor next period |
| 🔴 Red | Variance > 15% of budget | Escalate — requires management action plan |

## When to Override Thresholds

Standard thresholds may not be appropriate in all cases. Consider overriding when:

### Lower thresholds (more scrutiny)
- **New business lines**: less predictable, tighter monitoring needed
- **Regulatory items**: compliance costs should be closely tracked regardless of size
- **Cash-sensitive periods**: when liquidity is constrained, even small variances matter
- **Board-sensitive items**: anything the board has specifically asked to monitor

### Higher thresholds (less scrutiny)
- **Known one-offs**: if the variance is expected and already communicated
- **Timing differences**: if spend is budgeted in a different month but will net off over the quarter
- **Reclassifications**: if the variance is an accounting reclassification with no P&L impact

## Contextual Materiality

A variance's materiality depends on context, not just its size:

1. **Proportionality**: £50k on a £500k line (10%) is more material than £50k on a £5m line (1%)
2. **Trend**: A small variance that is growing month-on-month is more material than a large one-off
3. **Controllability**: Uncontrollable variances (e.g. exchange rates) need different treatment than controllable ones
4. **Cumulative effect**: Several small variances in the same direction may be collectively material
5. **Forecast impact**: A variance that affects the full-year forecast is more material than a timing difference

## Reporting Requirements by RAG Status

### 🟢 Green Items
- Listed in summary table (no commentary required)
- Grouped as "within tolerance" in the report

### 🟡 Amber Items
- Individual commentary required
- Must explain the driver
- Must state whether expected to continue or reverse
- Monitor in next period

### 🔴 Red Items
- Detailed commentary required with waterfall analysis
- Must include root cause analysis
- Must include management action plan
- Must include forecast impact assessment
- Escalate to senior management / board if persistent
