# Financial Forecasting & Variance Analysis Agent Template

A multi-agent workflow for generating financial forecasts, analysing budget variances, and producing management commentary using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. Combines numerical reasoning with plain-English narrative explanation.

## Architecture

```
Financial Data (Actuals, Budgets, Prior Periods)
      │
      ▼
┌─────────────────┐
│  Data Ingester   │ ── parse, normalise, extract KPIs
│   Sub-Agent      │
└────────┬────────┘
         │ ingester-output.yaml
         ▼
┌─────────────────┐
│  Trend Analyser  │ ── variances, growth rates, anomalies
│   Sub-Agent      │
└────────┬────────┘
         │ analyser-output.yaml
         ▼
┌─────────────────┐
│   Forecaster     │ ── projections, scenarios, confidence intervals
│   Sub-Agent      │
└────────┬────────┘
         │ forecaster-output.yaml
         ▼
┌─────────────────┐
│ Narrative Writer │ ── management commentary, driver analysis
│   Sub-Agent      │
└────────┬────────┘
         │ narrative-output.yaml
         ▼
    ┌──────────┐
    │  HUMAN   │ ── review, approve, distribute
    │  REVIEW  │
    └──────────┘
         │
         ▼
   Final Report
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Data Ingester** | Haiku | Raw financial data | `specs/ingester-output.yaml` | Parse data, normalise formats, extract KPIs |
| **Trend Analyser** | Sonnet | Ingester output | `specs/analyser-output.yaml` | Calculate variances, identify trends & anomalies |
| **Forecaster** | Sonnet | Ingester + Analyser output | `specs/forecaster-output.yaml` | Generate multi-scenario projections |
| **Narrative Writer** | Sonnet | All previous outputs | `specs/narrative-output.yaml` | Write plain-English management commentary |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines the complete report package after human review.

## Key Features

- **Multi-scenario forecasting** — best, base, and worst case with confidence intervals
- **Materiality-based variance flagging** — configurable thresholds (% and absolute)
- **Seasonal adjustment** — detects and applies seasonal patterns
- **Waterfall analysis** — breaks down key variances by driver
- **Plain-English commentary** — management-ready narrative, not just numbers
- **Report types** — monthly variance, quarterly forecast, annual budget review

## Usage

```bash
# Run the full pipeline on monthly P&L data
claude-code --agent CLAUDE.md \
  --input financial-data.txt \
  --output output/

# Run a single sub-agent (e.g. for testing)
claude-code --agent .claude/agents/data-ingester.md \
  --input financial-data.txt \
  --output ingester-output.yaml
```

## Human Review Gate

The pipeline pauses after the Narrative Writer. The human sees:
- Executive summary (2-3 sentence headline)
- Key variances with materiality flags
- Forecast scenarios (best/base/worst)
- Management commentary with recommended actions
- Risk and opportunity highlights

Actions: **Approve** (distribute as-is), **Edit** (modify commentary), **Request Reanalysis** (adjust assumptions), **Escalate** (flag for CFO/board attention).

## Customisation

- `specs/` — Modify output schemas to match your reporting structure
- `.claude/agents/` — Adjust agent prompts, materiality logic, narrative style
- `knowledge-base/` — Add your KPI definitions, thresholds, report templates
- `config.yaml` — Currency, thresholds, forecast horizon, scenario parameters

## ROI Estimate

| Metric | Value |
|--------|-------|
| Use case frequency | 5+ analyses/week |
| Staff cost replaced | £65/hr finance analyst time |
| Time per analysis (manual) | ~4 hours |
| Time per analysis (with agent) | ~30 minutes (review only) |
| Estimated weekly saving | ~17.5 hours / ~£1,137 |

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for analysis agents, Haiku for ingestion)

## Licence

MIT
