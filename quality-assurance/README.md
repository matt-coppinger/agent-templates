# Quality Assurance Analysis Agent Template

A multi-agent workflow for analysing quality data, identifying defect patterns, and generating QA reports using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. Designed for operations teams running 50+ analyses per week.

## Architecture

```
Quality Data Input
(defect reports, test results, inspection logs)
      │
      ▼
┌─────────────┐
│  Data Parser  │ ── structured metrics, defect extraction
│  Sub-Agent    │
└──────┬──────┘
       │ parser-output.yaml
       ▼
┌─────────────┐
│   Pattern    │ ── trends, clusters, correlations
│  Detector    │
└──────┬──────┘
       │ pattern-output.yaml
       ▼
┌─────────────┐
│  Root Cause  │ ── 5 Whys, Ishikawa, hypotheses
│  Analyser    │
└──────┬──────┘
       │ root-cause-output.yaml
       ▼
┌─────────────┐
│   Report     │ ── executive summary, Pareto, KPIs
│  Generator   │
└──────┬──────┘
       │ report-output.yaml
       ▼
  ┌──────────┐
  │  HUMAN   │ ── review, approve, action
  │  REVIEW  │
  └──────────┘
       │
       ▼
  Final QA Report
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Data Parser** | Haiku | Raw quality data | `specs/parser-output.yaml` | Parse defect reports, extract structured metrics |
| **Pattern Detector** | Haiku | Parser output | `specs/pattern-output.yaml` | Identify trends, clusters, correlations |
| **Root Cause Analyser** | Sonnet | Parser + Pattern output | `specs/root-cause-output.yaml` | Apply RCA frameworks, generate hypotheses |
| **Report Generator** | Sonnet | All previous outputs | `specs/report-output.yaml` | Generate comprehensive QA report |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines what the orchestrator produces after human approval.

## Usage

```bash
# Run the full pipeline on quality data
claude-code --agent agents/orchestrator.md \
  --input defect-data.txt \
  --output report/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/data-parser.md \
  --input defect-data.txt \
  --output parser-output.yaml
```

## Human Review Gate

The pipeline pauses after the Report Generator sub-agent. The human sees:
- Executive summary with key findings
- Pareto analysis (top 20% defects causing 80% of issues)
- Trend data across time periods
- Root cause hypotheses with confidence levels
- Recommended corrective actions with priority ratings
- KPI dashboard data

Actions: **Approve** (publish report), **Edit** (modify findings), **Reject** (re-analyse with feedback), **Escalate** (route to quality manager).

## Key Features

- **Pareto Analysis** — Identify the 20% of defect types causing 80% of quality issues
- **Trend Detection** — Spot patterns across shifts, lines, suppliers, and time periods
- **Root Cause Frameworks** — Automated 5 Whys and Ishikawa/fishbone analysis
- **Corrective Action Tracking** — Suggested CAPAs with priority and ownership
- **KPI Dashboard Data** — First pass yield, defect rate, DPMO, cost of quality

## Customisation

- `specs/` — Modify output schemas to match your data model
- `agents/` — Adjust analysis prompts, frameworks, thresholds
- `knowledge-base/` — Add your defect taxonomies, acceptance criteria, standards
- `config.yaml` — Pipeline settings (severity definitions, KPI thresholds, report format)

## ROI Estimate

| Metric | Manual | With Agent | Saving |
|--------|--------|------------|--------|
| Time per analysis | ~45 min | ~5 min | ~89% |
| Weekly analyses | 50 | 50 | — |
| Staff cost | $50/hr | — | — |
| **Weekly saving** | — | — | **$1,667** |
| **Annual saving** | — | — | **$86,667** |

## Requirements

- Claude Code CLI
- Access to Claude API (Haiku for parsing/detection, Sonnet for analysis/reporting)

## Licence

MIT
