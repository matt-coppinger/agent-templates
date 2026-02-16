# HR Policy & Benefits Q&A Agent Template

A multi-agent workflow for answering employee questions about HR policies, benefits, leave entitlements, and procedures using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. Sensitive topics (grievance, disciplinary) automatically escalate to a real HR person.

## Business Case

- **Use case:** RAG-based HR policy chatbot for medium organisations
- **Volume:** 50+ employee queries per week
- **Cost saving:** £40/hr HR staff time redirected from routine questions
- **ROI:** Self-service for ~80% of policy questions, freeing HR for complex casework

## Architecture

```
Employee Question
       │
       ▼
┌──────────────────┐
│ Intent Classifier │ ── topic, sensitivity level, personalisation needs
│    (Haiku)        │
└───────┬──────────┘
        │ classifier-output.yaml
        ▼
┌──────────────────┐
│ Policy Retriever  │ ── searches policy docs, extracts relevant rules
│    (Haiku)        │
└───────┬──────────┘
        │ retriever-output.yaml
        ▼
┌──────────────────┐
│Response Generator │ ── empathetic answer with citations & action steps
│    (Sonnet)       │
└───────┬──────────┘
        │ generator-output.yaml
        ▼
┌──────────────────┐
│Compliance Checker │ ── accuracy check, sensitivity flags, no legal advice
│    (Sonnet)       │
└───────┬──────────┘
        │ compliance-output.yaml
        ▼
   ┌──────────┐
   │ DELIVERY │ ── answer to employee (or escalate to HR)
   └──────────┘
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Intent Classifier** | Haiku | Raw question | `specs/classifier-output.yaml` | Classify topic, detect sensitivity, check if personalised data needed |
| **Policy Retriever** | Haiku | Classifier output + knowledge base | `specs/retriever-output.yaml` | Find relevant policy sections, extract rules and entitlements |
| **Response Generator** | Sonnet | Classifier + Retriever output | `specs/generator-output.yaml` | Draft clear, empathetic answer with citations |
| **Compliance Checker** | Sonnet | All previous outputs | `specs/compliance-output.yaml` | Verify accuracy, flag sensitive areas, block legal advice |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines what the orchestrator produces after compliance checking.

## Usage

```bash
# Run the full pipeline on an employee question
claude-code --agent agents/orchestrator.md \
  --input question.txt \
  --output response/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/classifier.md \
  --input question.txt \
  --output classifier-output.yaml
```

## Sensitivity Escalation

The pipeline short-circuits to a human HR person when:
- Topic is **grievance** or **disciplinary** (auto-escalate, no AI response)
- Sensitivity level is **high** or **critical**
- Question involves **redundancy**, **termination**, or **legal proceedings**
- Compliance checker flags **legal advice risk**

## Key Features

- **"I don't know" honesty** — if the policy doesn't cover the question, the agent says so rather than guessing
- **UK employment law awareness** — understands statutory minimums vs company enhancements
- **Empathetic tone** — acknowledges the employee's situation before providing information
- **Policy citations** — every answer references the specific policy section
- **Action steps** — tells employees exactly what to do next and who to contact

## Customisation

- `specs/` — Modify output schemas to match your data model
- `.claude/agents/` — Adjust system prompts, tone, policies
- `knowledge-base/` — Add your company's HR policies, benefits docs, contacts
- `config.yaml` — Pipeline settings (sensitivity thresholds, escalation contacts, language)

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for generator/compliance, Haiku for classifier/retriever)

## Licence

MIT
