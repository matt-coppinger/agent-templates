# Regulatory Change Monitoring Agent Template

A multi-agent workflow for tracking regulatory updates, summarising changes, and assessing organisational impact using Claude Code. Each sub-agent specialises in one stage of the pipeline, producing structured YAML output that feeds the next stage. Designed for scheduled (daily/weekly) operation with deduplication and urgency alerting.

## Business Case

- **5+ regulatory updates/week** at medium-sized organisations
- **$95/hr** average legal/compliance staff cost
- **80%+ time savings** on routine regulatory scanning and initial impact assessment
- Consistent, auditable analysis across all regulatory domains

## Architecture

```
Regulatory Feeds / Bulletins
           │
           ▼
  ┌────────────────┐
  │  Feed Scanner   │ ── extract new regulations, amendments, deadlines
  │   (Haiku)       │    categorise by domain
  └───────┬────────┘
          │ scanner-output.yaml
          ▼
  ┌────────────────┐
  │ Change Analyser │ ── what's new vs current, effective dates,
  │   (Sonnet)      │    transition periods, penalties
  └───────┬────────┘
          │ analyser-output.yaml
          ▼
  ┌────────────────┐
  │ Impact Assessor │ ── departments affected, policy changes needed,
  │   (Sonnet)      │    implementation effort, risk rating
  └───────┬────────┘
          │ assessor-output.yaml
          ▼
  ┌────────────────┐
  │ Briefing Writer │ ── executive summary, action items with owners,
  │   (Sonnet)      │    compliance timeline, recommendations
  └───────┬────────┘
          │ briefing-output.yaml
          ▼
     ┌──────────┐
     │  OUTPUT   │ ── executive briefing + alerts
     │  & ALERTS │
     └──────────┘
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Feed Scanner** | Haiku | Raw bulletins/feeds | `specs/scanner-output.yaml` | Parse feeds, extract changes, categorise by domain |
| **Change Analyser** | Sonnet | Scanner output + knowledge base | `specs/analyser-output.yaml` | Analyse what's changed vs current requirements |
| **Impact Assessor** | Sonnet | Analyser output + department mapping | `specs/assessor-output.yaml` | Assess organisational impact per department |
| **Briefing Writer** | Sonnet | All previous outputs | `specs/briefing-output.yaml` | Generate executive briefing with action items |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines the complete pipeline output including audit trail.

## Usage

```bash
# Run the full pipeline on a regulatory bulletin
claude-code --agent CLAUDE.md \
  --input examples/sample-bulletin.txt \
  --output output/

# Run a single sub-agent (e.g. for testing)
claude-code --agent .claude/agents/feed-scanner.md \
  --input bulletin.txt \
  --output scanner-output.yaml

# Scheduled daily run (cron/task scheduler)
claude-code --agent CLAUDE.md \
  --input feeds/ \
  --output output/$(date +%Y-%m-%d)/
```

## Key Features

- **Scheduled monitoring** — designed for daily/weekly automated runs, not just one-shot
- **Deduplication** — tracks previously processed changes to avoid duplicate alerts
- **Urgency alerting** — immediate notification for breaking regulatory changes
- **Compliance calendar** — tracks key regulatory dates and deadlines
- **Action items** — generates specific tasks with department owners and deadlines
- **Multi-domain** — data protection, employment, financial, health & safety, environmental

## Customisation

- `config.yaml` — Jurisdiction, domains to monitor, alert thresholds, briefing frequency
- `specs/` — Modify output schemas to match your compliance data model
- `.claude/agents/` — Adjust system prompts, analysis depth, writing style
- `knowledge-base/` — Add your organisation's regulatory baselines and department structure

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for analysis agents, Haiku for scanner)

## Licence

MIT
