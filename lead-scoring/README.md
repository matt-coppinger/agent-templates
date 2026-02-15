# Lead Scoring Agent Template

A multi-agent workflow for scoring and routing inbound leads using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. Leads are enriched, scored, qualified, and routed to the right sales team with suggested talking points.

## Architecture

```
Inbound Lead
      │
      ▼
┌─────────────┐
│   Enricher   │ ── firmographic data, intent signals, tech stack
│  Sub-Agent   │
└──────┬──────┘
       │ enricher-output.yaml
       ▼
┌─────────────┐
│    Scorer    │ ── weighted scoring across 4 dimensions (0-100)
│  Sub-Agent   │
└──────┬──────┘
       │ scorer-output.yaml
       ▼
┌─────────────┐
│  Qualifier   │ ── hot / warm / cold / disqualified + rationale
│  Sub-Agent   │
└──────┬──────┘
       │ qualifier-output.yaml
       ▼
┌─────────────┐
│    Router    │ ── team, action, priority, talking points
│  Sub-Agent   │
└──────┬──────┘
       │ router-output.yaml
       ▼
  ┌──────────┐
  │  FINAL   │ ── consolidated output + audit trail
  │  OUTPUT  │
  └──────────┘
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Enricher** | Haiku | Raw lead data | `specs/enricher-output.yaml` | Enrich with firmographic/behavioural data, extract intent |
| **Scorer** | Haiku | Enricher output + scoring model | `specs/scorer-output.yaml` | Apply weighted scoring (firmographic, behavioural, intent, timing) |
| **Qualifier** | Sonnet | Enricher + Scorer output | `specs/qualifier-output.yaml` | Classify lead tier + provide qualification rationale |
| **Router** | Sonnet | All previous outputs | `specs/router-output.yaml` | Route to sales team, recommend action, suggest talking points |

## Scoring Dimensions

| Dimension | Weight | Range | What It Measures |
|-----------|--------|-------|------------------|
| Firmographic Fit | 30% | 0–30 | Company size, industry, revenue match to ICP |
| Behavioural Signals | 25% | 0–25 | Source channel, content engagement, website activity |
| Intent Signals | 25% | 0–25 | Message content, buying language, urgency indicators |
| Timing & Urgency | 20% | 0–20 | Budget cycle, stated timeline, competitive evaluation |

**Total: 0–100**

## Qualification Tiers

| Tier | Score Range | Action |
|------|-------------|--------|
| 🔥 Hot Lead | 75–100 | Immediate outreach — sales call within 4 hours |
| 🟡 Warm Lead | 50–74 | Personalised nurture sequence — email within 24 hours |
| 🔵 Cold Lead | 25–49 | Long-term nurture — add to drip campaign |
| ⛔ Disqualified | 0–24 (or criteria match) | Log reason, no sales action |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines the consolidated pipeline output.

## Usage

```bash
# Run the full pipeline on a lead
claude-code --agent CLAUDE.md \
  --input examples/sample-lead.txt

# Run a single sub-agent (e.g. for testing)
claude-code --agent .claude/agents/enricher.md \
  --input examples/sample-lead.txt
```

## Customisation

- `specs/` — Modify output schemas to match your CRM data model
- `.claude/agents/` — Adjust system prompts, scoring logic, routing rules
- `knowledge-base/` — Add your ICP documents, scoring criteria, disqualification rules
- `config.yaml` — Pipeline settings (scoring weights, thresholds, team routing)

## Requirements

- Claude Code CLI
- Access to Claude API (Haiku for enricher/scorer, Sonnet for qualifier/router)

## Licence

MIT
