# Due Diligence Document Analysis Agent Template

A multi-agent workflow for analysing M&A data room documents using Claude Code. Each sub-agent specialises in one stage of the due diligence pipeline, producing structured YAML output that feeds the next stage. A mandatory human review gate ensures no findings are actioned without legal professional approval.

> **⚠️ Disclaimer:** This tool assists with document analysis only. It does not constitute legal, financial, or tax advice. All outputs must be reviewed by qualified professionals before reliance.

## Architecture

```
Data Room Documents
        │
        ▼
┌───────────────┐
│   Document    │ ── catalogue, classify, extract metadata,
│    Indexer    │    flag missing documents
└───────┬───────┘
        │ indexer-output.yaml
        ▼
┌───────────────┐
│     Risk      │ ── deep-read by category, extract material
│   Extractor   │    risks, rate severity (RAG)
└───────┬───────┘
        │ risk-extractor-output.yaml
        ▼
┌───────────────┐
│    Cross-     │ ── cross-reference findings, detect
│  Referencer   │    contradictions, gaps, hidden liabilities
└───────┬───────┘
        │ cross-referencer-output.yaml
        ▼
┌───────────────┐
│    Report     │ ── executive summary, risk register,
│    Writer     │    deal-breaker flags, recommendations
└───────┬───────┘
        │ report-writer-output.yaml
        ▼
   ┌──────────┐
   │  HUMAN   │ ── review, amend, approve, or reject
   │  REVIEW  │
   └──────────┘
        │
        ▼
   Final DD Report
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Document Indexer** | Haiku | Raw data room files | `specs/indexer-output.yaml` | Catalogue documents, classify by type, extract metadata, flag gaps |
| **Risk Extractor** | Sonnet | Indexer output + documents | `specs/risk-extractor-output.yaml` | Extract material risks per category, rate severity |
| **Cross-Referencer** | Sonnet | Indexer + Risk outputs | `specs/cross-referencer-output.yaml` | Cross-reference findings, detect contradictions and gaps |
| **Report Writer** | Sonnet | All previous outputs | `specs/report-writer-output.yaml` | Generate structured DD report with risk register |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines the complete DD report package after human approval.

## Usage

```bash
# Run the full pipeline on a data room
claude-code --agent agents/orchestrator.md \
  --input data-room/ \
  --output output/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/document-indexer.md \
  --input data-room/ \
  --output indexer-output.yaml
```

## Human Review Gate

The pipeline pauses after the Report Writer. The reviewing professional sees:
- Document index with completeness assessment
- Risk register with RAG status (Red/Amber/Green)
- Deal-breaker flags requiring immediate attention
- Cross-referencing findings (contradictions, gaps)
- Recommended conditions, warranties, and further investigation areas

Actions: **Approve** (accept report), **Amend** (modify findings), **Reject** (back to pipeline with feedback), **Escalate** (route to specialist counsel).

## Key Features

- **Data room completeness check** — expected vs present documents by category
- **Risk register with RAG status** — Red (deal-breaker), Amber (material concern), Green (acceptable)
- **Deal-breaker flagging** — automatic escalation of critical findings
- **Cross-document contradiction detection** — identifies inconsistencies across document categories
- **Always-human-review** — no output is finalised without professional sign-off
- **Audit trail** — full traceability of every finding back to source documents

## Customisation

- `specs/` — Modify output schemas to match your firm's reporting format
- `agents/` — Adjust analysis depth, risk thresholds, jurisdiction-specific rules
- `knowledge-base/` — Add checklists, risk taxonomies, standard clause libraries
- `config.yaml` — Pipeline settings (jurisdiction, risk definitions, report format)

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for analysis agents, Haiku for indexer)

## Licence

MIT
