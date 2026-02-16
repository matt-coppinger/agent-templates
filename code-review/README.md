# Code Review Agent Template

A multi-agent workflow for automated PR code review using Claude Code. Each sub-agent specialises in one step of the review pipeline, producing structured YAML output that feeds the next stage. Designed for engineering teams doing 200+ reviews per week — at $75/hr engineer cost, even a 30% reduction in review time saves significant money.

## Architecture

```
PR Diff / Changeset
        │
        ▼
┌───────────────┐
│ Diff Analyser  │ ── parse diff, categorise changes, extract modifications
│  Sub-Agent     │
└───────┬───────┘
        │ diff-analysis-output.yaml
        ▼
┌───────────────┐
│  Bug Scanner   │ ── bugs, vulnerabilities, race conditions, error handling
│  Sub-Agent     │
└───────┬───────┘
        │ bug-scan-output.yaml
        ▼
┌───────────────┐
│ Style Checker  │ ── naming, docs, complexity, conventions
│  Sub-Agent     │
└───────┬───────┘
        │ style-check-output.yaml
        ▼
┌───────────────┐
│    Review      │ ── synthesise findings into actionable review comments
│   Composer     │
└───────┬───────┘
        │ review-output.yaml
        ▼
   ┌──────────┐
   │  HUMAN   │ ── approve, amend, or override findings
   │  REVIEW  │
   └──────────┘
        │
        ▼
   Final Review
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Diff Analyser** | Haiku | Raw diff/PR | `specs/diff-analysis-output.yaml` | Parse changes, categorise change types, extract key modifications |
| **Bug Scanner** | Sonnet | Diff analysis | `specs/bug-scan-output.yaml` | Find bugs, security issues, performance problems, race conditions |
| **Style Checker** | Haiku | Diff analysis + style guide | `specs/style-check-output.yaml` | Check naming, docs, complexity, conventions |
| **Review Composer** | Sonnet | All previous outputs | `specs/review-output.yaml` | Synthesise into prioritised, actionable review comments |

## Severity Levels

All findings use a consistent severity scale:

| Severity | Meaning | Action Required |
|----------|---------|-----------------|
| **critical** | Security vulnerability, data loss risk, production breakage | Must fix before merge |
| **major** | Bugs, significant performance issues, missing error handling | Should fix before merge |
| **minor** | Code smell, suboptimal approach, minor style violation | Fix recommended |
| **suggestion** | Improvement idea, alternative approach, nice-to-have | Optional |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines what the orchestrator produces after human review.

## Usage

```bash
# Run the full pipeline on a PR diff
claude-code --agent agents/orchestrator.md \
  --input pr-diff.txt \
  --output review/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/diff-analyser.md \
  --input pr-diff.txt \
  --output diff-analysis-output.yaml
```

## Human Review Gate

The pipeline pauses after the Review Composer. The human sees:
- Original diff summary
- Prioritised list of findings by severity
- Suggested fixes with code snippets
- Overall review verdict and confidence

Actions: **Approve** (post review as-is), **Edit** (modify comments), **Override** (dismiss findings), **Escalate** (flag for senior engineer).

## Customisation

- `specs/` — Modify output schemas to match your review workflow
- `agents/` — Adjust analysis depth, language support, strictness
- `knowledge-base/` — Add your style guides, security checklists, patterns
- `config.yaml` — Pipeline settings (severity thresholds, languages, style guide path)

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for Bug Scanner & Review Composer, Haiku for Diff Analyser & Style Checker)

## Licence

MIT
