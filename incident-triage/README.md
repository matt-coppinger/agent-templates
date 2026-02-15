# Incident Triage & Response Agent Template

A multi-agent workflow for triaging and responding to production incidents using Claude Code. Four sub-agents handle classification, investigation, response planning, and quality review — with a human review gate before any action is taken.

## Architecture

```
Incoming Incident
      │
      ▼
┌──────────────┐
│  Classifier   │ ── severity, category, affected systems, customer impact
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Investigator  │ ── searches runbooks, logs, past incidents, builds timeline
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  Responder    │ ── prioritised actions, RCA hypothesis, comms drafts
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  Reviewer     │ ── validates against runbooks, checks risks
└──────┬───────┘
       │
       ▼
  ┌──────────┐
  │  HUMAN   │ ── approve, modify, escalate
  │  REVIEW  │
  └──────────┘
```

## Sub-Agents

| Agent | Model | Purpose |
|-------|-------|---------|
| **Classifier** | Haiku | Rapid triage — severity, category, impact assessment |
| **Investigator** | Sonnet | Deep analysis — timeline, root cause hypotheses, runbook matching |
| **Responder** | Sonnet | Action planning — mitigation steps, RCA, internal/external comms |
| **Reviewer** | Sonnet | Quality gate — validates actions against runbooks and risk assessment |

## Key Features

- **Severity escalation** — P1 incidents bypass the pipeline and go straight to human
- **Runbook-driven** — investigator and reviewer validate against operational runbooks
- **Full incident timeline** — chronological reconstruction from all available sources
- **Multi-audience comms** — internal (Slack/Teams), customer (status page), and executive summary
- **Risk-assessed actions** — every action has a risk level, rollback plan, and owner
- **Audit trail** — complete YAML output from every stage saved to `output/{incident_id}/`

## Quick Start

```bash
cd incident-triage

# Add your runbooks
cp your-runbooks/* runbooks/

# Add architecture docs, past incidents, SLAs
cp your-docs/* knowledge-base/

# Run with Claude Code
claude
```

Then prompt:

```
Process the incident in examples/sample-incident.txt through the full pipeline.
```

## Customisation

- `runbooks/` — Add your operational runbooks (markdown)
- `knowledge-base/` — Architecture docs, past incidents, SLAs, scheduled events
- `config.yaml` — Severity thresholds, communication settings, model choices
- `specs/` — Modify output schemas to match your incident management system
- `.claude/agents/` — Adjust sub-agent prompts for your team's terminology and processes

## Requirements

- [Claude Code CLI](https://code.claude.com) installed and authenticated
- Claude API access (Sonnet recommended, Haiku for classification)
