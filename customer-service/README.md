# Customer Service Agent Template

A multi-agent workflow for handling customer service tickets using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. A human review gate ensures nothing goes to the customer without approval.

## Architecture

```
Incoming Ticket
      │
      ▼
┌─────────────┐
│  Classifier  │ ── sentiment, category, urgency
│  Sub-Agent   │
└──────┬──────┘
       │ classifier-output.yaml
       ▼
┌─────────────┐
│  Researcher  │ ── searches knowledge base, finds relevant docs
│  Sub-Agent   │
└──────┬──────┘
       │ research-output.yaml
       ▼
┌─────────────┐
│   Drafter    │ ── writes response using research + context
│  Sub-Agent   │
└──────┬──────┘
       │ draft-output.yaml
       ▼
┌─────────────┐
│   Reviewer   │ ── quality checks against tone/policy/accuracy
│  Sub-Agent   │
└──────┬──────┘
       │ review-output.yaml
       ▼
  ┌──────────┐
  │  HUMAN   │ ── approve, edit, or reject
  │  REVIEW  │
  └──────────┘
       │
       ▼
  Final Response
```

## Sub-Agents

| Agent | Input | Output Spec | Purpose |
|-------|-------|-------------|---------|
| **Classifier** | Raw ticket | `specs/classifier-output.yaml` | Categorise, assess sentiment & urgency, detect language |
| **Researcher** | Classifier output + knowledge base | `specs/research-output.yaml` | Find relevant docs, past tickets, policy references |
| **Drafter** | Classifier + Research output | `specs/draft-output.yaml` | Write customer-facing response |
| **Reviewer** | All previous outputs | `specs/review-output.yaml` | Quality gate before human review |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines what the orchestrator produces after human approval.

## Usage

```bash
# Run the full pipeline on a ticket
claude-code --agent agents/orchestrator.md \
  --input ticket.txt \
  --output response/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/classifier.md \
  --input ticket.txt \
  --output classifier-output.yaml
```

## Human Review Gate

The pipeline pauses after the Reviewer sub-agent. The human sees:
- Original ticket
- Classification summary
- Drafted response
- Reviewer's quality assessment and confidence score

Actions: **Approve** (send as-is), **Edit** (modify then send), **Reject** (back to drafter with feedback), **Escalate** (route to specialist).

## Customisation

- `specs/` — Modify output schemas to match your data model
- `agents/` — Adjust system prompts, tone, policies
- `knowledge-base/` — Add your company docs, FAQs, product guides
- `config.yaml` — Pipeline settings (escalation thresholds, language, tone)

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet recommended for sub-agents, Haiku for classifier)

## Licence

MIT
