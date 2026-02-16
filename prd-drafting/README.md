# PRD Drafting Agent Template

A multi-agent workflow for generating product requirement documents, technical specifications, and feature briefs from rough inputs using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. A revision loop between writer and reviewer ensures quality before human approval.

## Business Case

- **Use case:** Generate PRDs, tech specs, and feature briefs from user stories, meeting notes, feature requests, and Slack threads
- **Volume:** 10+ specs/week at medium organisations
- **Cost saving:** $70/hr product staff cost × 2–4 hrs per PRD = $140–280 per document
- **Output formats:** Full PRD, feature brief, technical specification

## Architecture

```
Raw Input (user stories, meeting notes, feature requests)
      │
      ▼
┌──────────────┐
│ Input Parser  │ ── requirements, constraints, stakeholders, success criteria
│  (Haiku)      │
└──────┬───────┘
       │ parser-output.yaml
       ▼
┌──────────────┐
│  Research     │ ── cross-reference existing PRDs, tech constraints, debt
│  Enricher    │
│  (Haiku)      │
└──────┬───────┘
       │ enricher-output.yaml
       ▼
┌──────────────┐
│ Spec Writer   │ ── structured PRD, feature brief, or tech spec
│  (Sonnet)     │
└──────┬───────┘
       │ writer-output.yaml
       ▼
┌──────────────┐
│  Reviewer     │ ── completeness, consistency, feasibility, testability
│  (Sonnet)     │
└──────┬───────┘
       │ reviewer-output.yaml
       │
       ├── verdict: pass ──────► Human Review ──► Final Output
       │
       └── verdict: revise ───► Back to Spec Writer (max 2 rounds)
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Input Parser** | Haiku | Raw input text | `specs/parser-output.yaml` | Extract requirements, constraints, stakeholders, success criteria, out-of-scope items |
| **Research Enricher** | Haiku | Parser output + knowledge base | `specs/enricher-output.yaml` | Cross-reference existing PRDs, technical constraints, API capabilities, design system, tech debt |
| **Spec Writer** | Sonnet | Parser + Enricher output | `specs/writer-output.yaml` | Generate structured document (PRD, feature brief, or tech spec) |
| **Reviewer** | Sonnet | All previous outputs | `specs/reviewer-output.yaml` | Completeness check, testability validation, consistency review, improvement suggestions |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines what the orchestrator produces after human approval.

## Usage

```bash
# Run the full pipeline on a feature request
claude-code --agent agents/orchestrator.md \
  --input feature-request.txt \
  --output output/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/input-parser.md \
  --input feature-request.txt \
  --output parser-output.yaml
```

## Key Features

- **Multiple output formats** — full PRD, lightweight feature brief, or technical spec
- **Requirement testability checking** — flags vague or untestable requirements
- **Given/When/Then acceptance criteria** — structured, verifiable criteria
- **NFR completeness validation** — checks against performance, security, accessibility, i18n checklist
- **Revision loop** — writer ↔ reviewer cycle (max 2 rounds) before human review

## Customisation

- `specs/` — Modify output schemas to match your data model
- `.claude/agents/` — Adjust system prompts, output formats, review criteria
- `knowledge-base/` — Add your existing PRDs, API docs, design system references
- `config.yaml` — Pipeline settings (output format, completeness thresholds, review weights)

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for writer/reviewer, Haiku for parser/enricher)

## Licence

MIT
