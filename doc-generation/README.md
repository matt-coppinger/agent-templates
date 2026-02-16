# Documentation Generation Agent Template

A multi-agent workflow for generating and maintaining technical documentation from source code using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. Supports multiple doc types: API references, tutorials, runbooks, and architecture documents.

## Business Case

- **Use case:** Generate and maintain technical documentation, API docs, and runbooks from code and comments
- **Volume:** 15+ docs/week at medium engineering organisations
- **Cost saved:** ~$75/hr engineer time redirected from manual documentation
- **Doc types:** API reference, tutorial, runbook, architecture document

## Architecture

```
Source Code / Comments
        │
        ▼
┌───────────────┐
│ Code Analyser  │ ── signatures, classes, dependencies, inline docs
│   Sub-Agent    │
└───────┬───────┘
        │ analyser-output.yaml
        ▼
┌───────────────┐
│   Structure    │ ── doc type, sections, gaps, cross-references
│   Planner      │
└───────┬───────┘
        │ planner-output.yaml
        ▼
┌───────────────┐
│  Doc Writer    │ ── full documentation with examples & diagrams
│   Sub-Agent    │
└───────┬───────┘
        │ writer-output.yaml
        ▼
┌───────────────┐
│   Quality      │ ── accuracy, completeness, readability, consistency
│   Reviewer     │
└───────┬───────┘
        │ reviewer-output.yaml
        ▼
   ┌──────────┐
   │  HUMAN   │ ── approve, edit, or reject
   │  REVIEW  │
   └──────────┘
        │
        ▼
  Final Documentation
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Code Analyser** | Haiku | Raw source code | `specs/analyser-output.yaml` | Parse code, extract signatures, classes, dependencies, inline docs |
| **Structure Planner** | Haiku | Analyser output | `specs/planner-output.yaml` | Determine doc type, plan sections, identify gaps |
| **Doc Writer** | Sonnet | Analyser + Planner output | `specs/writer-output.yaml` | Generate documentation with examples and cross-references |
| **Quality Reviewer** | Sonnet | All previous outputs | `specs/reviewer-output.yaml` | Check accuracy, completeness, readability, consistency |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines what the orchestrator produces after human approval.

## Key Features

- **Multiple doc types** — API reference, tutorial, runbook, architecture document
- **Code example generation** — Working examples derived from source code
- **Cross-reference linking** — Automatic links between related documentation
- **Versioning awareness** — Tracks API versions, deprecations, and changelogs
- **Diff-based updates** — Only regenerates sections where source code has changed
- **Template-driven** — Consistent structure via `knowledge-base/templates/`

## Usage

```bash
# Run the full pipeline on source code
claude-code --agent agents/orchestrator.md \
  --input src/ \
  --output docs/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/code-analyser.md \
  --input src/api/users.py \
  --output analyser-output.yaml
```

## Human Review Gate

The pipeline pauses after the Quality Reviewer sub-agent. The human sees:
- Source code summary
- Planned documentation structure
- Generated documentation
- Quality assessment and confidence score

Actions: **Approve** (publish as-is), **Edit** (modify then publish), **Reject** (back to writer with feedback), **Regenerate** (re-run from a specific stage).

## Customisation

- `specs/` — Modify output schemas to match your documentation standards
- `.claude/agents/` — Adjust system prompts, coding conventions, doc style
- `knowledge-base/templates/` — Add or modify documentation templates
- `knowledge-base/style/` — Technical writing style guide
- `config.yaml` — Pipeline settings (models, languages, output format)

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for writer/reviewer, Haiku for analyser/planner)

## Licence

MIT
