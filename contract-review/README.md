# Contract Review Agent Template

A multi-agent workflow for reviewing contracts, extracting key clauses, assessing risk, and generating executive summaries using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. A mandatory human review gate ensures no legal output is ever auto-approved.

> **⚠️ Disclaimer:** This tool assists with contract review but does **not** constitute legal advice. All output must be reviewed by a qualified legal professional before any action is taken.

## Business Case

- **Use case:** Review contracts for key terms, flag non-standard or risky clauses, extract structured data, generate review summaries
- **Volume:** 20+ contracts/week at medium organisations
- **Cost saving:** $95/hr legal staff cost — automates initial review, clause extraction, and risk triage
- **Jurisdiction:** UK default (configurable)

## Architecture

```
Incoming Contract
       │
       ▼
┌──────────────────┐
│  Clause Extractor │ ── parse contract, identify & extract key clauses
│    Sub-Agent      │
└────────┬─────────┘
         │ clause-extractor-output.yaml
         ▼
┌──────────────────┐
│  Risk Assessor    │ ── evaluate clauses against playbook, rate risk
│    Sub-Agent      │
└────────┬─────────┘
         │ risk-assessor-output.yaml
         ▼
┌──────────────────┐
│   Comparator      │ ── compare against templates/precedents
│    Sub-Agent      │
└────────┬─────────┘
         │ comparator-output.yaml
         ▼
┌──────────────────┐
│  Summary Writer   │ ── executive summary, risk heat map, actions
│    Sub-Agent      │
└────────┬─────────┘
         │ summary-writer-output.yaml
         ▼
    ┌──────────┐
    │  HUMAN   │ ── review, approve, or escalate (ALWAYS required)
    │  REVIEW  │
    └──────────┘
         │
         ▼
   Final Review Output
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Clause Extractor** | Sonnet | Raw contract text | `specs/clause-extractor-output.yaml` | Parse and extract key clauses with metadata |
| **Risk Assessor** | Sonnet | Extracted clauses + playbook | `specs/risk-assessor-output.yaml` | Rate risk per clause, flag deviations, detect missing clauses |
| **Comparator** | Haiku | Extracted clauses + templates | `specs/comparator-output.yaml` | Compare against standard precedents, note differences |
| **Summary Writer** | Sonnet | All previous outputs | `specs/summary-writer-output.yaml` | Executive summary with risk heat map and recommendations |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines what the orchestrator produces after human review.

## Usage

```bash
# Run the full pipeline on a contract
claude-code --agent agents/orchestrator.md \
  --input contract.txt \
  --output review/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/clause-extractor.md \
  --input contract.txt \
  --output clause-extractor-output.yaml
```

## Human Review Gate

The pipeline **always** pauses before producing final output. The human sees:
- Original contract reference
- Extracted clauses summary
- Risk heat map (clause-by-clause: high/medium/low)
- Comparison against standard templates
- Executive summary with recommended actions

Actions: **Approve** (accept review as-is), **Edit** (modify findings), **Escalate** (route to senior counsel), **Request Re-review** (back to pipeline with guidance).

**Legal output is never auto-approved.** The `always_review` setting cannot be overridden.

## Key Features

- **Risk heat map** — clause-by-clause risk rating (high/medium/low) with visual summary
- **Missing clause detection** — flags standard clauses absent from the contract
- **Red flag alerting** — clauses that always require senior review
- **Jurisdiction awareness** — UK default, configurable per review
- **Negotiation talking points** — leverage points and recommended positions
- **Audit trail** — full traceability of each pipeline stage

## Customisation

- `specs/` — Modify output schemas to match your data model
- `agents/` — Adjust system prompts, clause categories, risk criteria
- `knowledge-base/` — Add your firm's playbooks, templates, precedents
- `config.yaml` — Pipeline settings (jurisdiction, risk thresholds, clause checklist)

## Knowledge Base

```
knowledge-base/
├── playbook/
│   ├── standard-clauses.md    # Standard clause playbook (UK commercial)
│   └── red-flag-clauses.md    # Clauses requiring senior review
├── templates/
│   └── standard-nda.md        # Sample NDA for comparison
└── reference/
    └── governing-law-notes.md # Jurisdiction considerations
```

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for most agents, Haiku for comparator)

## Licence

MIT
