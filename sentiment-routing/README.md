# Sentiment Routing Agent Template

A multi-agent workflow for analysing customer message sentiment and routing tickets to the right team using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. Designed for high-volume customer service operations (200+ messages/week) where accurate prioritisation saves real money ($35/hr staff cost).

## Architecture

```
Incoming Message
      │
      ▼
┌─────────────────┐
│ Emotion Detector │ ── emotions, key phrases, tone signals
│   Sub-Agent      │
└────────┬────────┘
         │ emotion-output.yaml
         ▼
┌─────────────────┐
│ Context Assessor │ ── account value, history, churn risk
│   Sub-Agent      │
└────────┬────────┘
         │ context-output.yaml
         ▼
┌─────────────────┐
│ Priority Scorer  │ ── P1-P4 score, escalation recommendation
│   Sub-Agent      │
└────────┬────────┘
         │ priority-output.yaml
         ▼
┌─────────────────┐
│     Router       │ ── team, SLA, handling approach, de-escalation
│   Sub-Agent      │
└────────┬────────┘
         │ routing-output.yaml
         ▼
    ┌──────────┐
    │  HUMAN   │ ── confirm routing, override if needed
    │  REVIEW  │
    └──────────┘
         │
         ▼
   Ticket Routed
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Emotion Detector** | Haiku | Raw message | `specs/emotion-output.yaml` | Detect emotions, extract sentiment-signalling phrases |
| **Context Assessor** | Haiku | Emotion output + customer data | `specs/context-output.yaml` | Assess account value, history, churn risk |
| **Priority Scorer** | Sonnet | Emotion + Context outputs | `specs/priority-output.yaml` | Calculate P1-P4 priority, recommend escalation |
| **Router** | Sonnet | All previous outputs | `specs/routing-output.yaml` | Determine team, SLA, handling approach, de-escalation notes |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines what the orchestrator produces after human confirmation.

## Usage

```bash
# Run the full pipeline on a customer message
claude-code --agent agents/orchestrator.md \
  --input message.txt \
  --output routing/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/emotion-detector.md \
  --input message.txt \
  --output emotion-output.yaml
```

## Human Review Gate

The pipeline pauses after the Router sub-agent. The human sees:
- Original message
- Emotion analysis summary
- Priority score and rationale
- Recommended team, SLA, and handling approach
- De-escalation talking points (if applicable)

Actions: **Confirm** (route as recommended), **Override** (change team/priority), **Escalate** (immediate manager attention).

## Key Features

- **VIP customer detection** — high-value accounts flagged for priority handling
- **Churn risk flagging** — at-risk customers identified from language and history signals
- **De-escalation talking points** — ready-made guidance for the receiving agent
- **P1 short-circuit** — safety/legal threats bypass the full pipeline for immediate escalation
- **Automatic P1 escalation** — no human delay for critical threats

## Customisation

- `specs/` — Modify output schemas to match your data model
- `agents/` — Adjust detection rules, thresholds, tone policies
- `knowledge-base/` — Add your team directory, escalation policies, SLA definitions
- `config.yaml` — Pipeline settings (priority thresholds, team routing, SLA targets)

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for Priority Scorer and Router, Haiku for Emotion Detector and Context Assessor)

## Licence

MIT
