# CV Screening & Shortlisting Agent Template

A multi-agent workflow for screening job applications using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. Bias mitigation is built in — no names, ages, or gender are passed to scoring agents.

## Use Case

Medium organisations receiving 50+ applications per week. At £40/hr HR staff cost, manual screening of 50 CVs takes ~12 hours/week. This pipeline reduces that to minutes of review time, with consistent, auditable scoring.

## Architecture

```
Batch of CVs + Job Specification
              │
              ▼
     ┌────────────────┐
     │     Parser      │ ── extract structured data (anonymised)
     │   (Haiku)       │
     └───────┬────────┘
             │ parser-output.yaml (per CV)
             ▼
     ┌────────────────┐
     │     Matcher     │ ── score against requirements
     │   (Haiku)       │
     └───────┬────────┘
             │ matcher-output.yaml (per CV)
             ▼
     ┌────────────────┐
     │    Assessor     │ ── holistic assessment, red flags, trajectory
     │   (Sonnet)      │
     └───────┬────────┘
             │ assessor-output.yaml (per CV)
             ▼
     ┌────────────────┐
     │     Ranker      │ ── rank batch, generate shortlist
     │   (Sonnet)      │
     └───────┬────────┘
             │ ranker-output.yaml (batch)
             ▼
        ┌──────────┐
        │  HUMAN   │ ── review shortlist, approve interviews
        │  REVIEW  │
        └──────────┘
             │
             ▼
      Final Shortlist + Interview Focus Areas
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Parser** | Haiku | Raw CV text | `specs/parser-output.yaml` | Extract structured data, anonymise personal details |
| **Matcher** | Haiku | Parsed CV + job spec | `specs/matcher-output.yaml` | Score against must-have/nice-to-have requirements |
| **Assessor** | Sonnet | Parsed CV + match scores | `specs/assessor-output.yaml` | Career trajectory, cultural signals, red flags |
| **Ranker** | Sonnet | All assessments in batch | `specs/ranker-output.yaml` | Rank candidates, generate shortlist with interview focus |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines the complete shortlist package after human review.

## Usage

```bash
# Run the full pipeline on a batch of CVs
claude-code --agent agents/orchestrator.md \
  --input cvs/ \
  --output output/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/parser.md \
  --input cv.txt \
  --output parser-output.yaml
```

## Bias Mitigation

This pipeline is designed to reduce unconscious bias:

- **Anonymisation**: The Parser strips names, ages, gender, photos, and addresses before any scoring occurs
- **Structured scoring**: The Matcher uses objective criteria only (skills, experience, qualifications)
- **Configurable weighting**: Must-have vs nice-to-have weights are set in `config.yaml`, not left to individual judgement
- **Audit trail**: Every score and decision is recorded with reasoning for later review
- **Policy compliance**: The Assessor reads `knowledge-base/policies/hiring-policy.md` for organisational guidelines

## Customisation

- `specs/` — Modify output schemas to match your data model
- `agents/` — Adjust system prompts, scoring criteria, assessment focus
- `knowledge-base/` — Add job specifications, hiring policies, skills taxonomies
- `config.yaml` — Pipeline settings (weights, shortlist size, bias mitigation)

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for assessor/ranker, Haiku for parser/matcher)

## Licence

MIT
