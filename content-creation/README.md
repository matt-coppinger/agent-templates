# Content Creation Pipeline Agent Template

A multi-agent workflow for generating marketing content using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. A revision loop between writer and editor ensures quality before final delivery.

## ROI Case

- **Use case:** Blog posts, social media, email campaigns, marketing copy
- **Throughput:** 15+ pieces/week at medium organisations
- **Staff cost replaced:** $55/hr marketing content staff
- **Estimated saving:** ~$3,500/month at 15 pieces/week

## Architecture

```
Content Brief
      │
      ▼
┌────────────────┐
│ Brief Analyser │ ── target audience, key messages, tone, SEO keywords
│   (Haiku)      │
└───────┬────────┘
        │ brief-analysis.yaml
        ▼
┌────────────────┐
│   Research     │ ── statistics, angles, competitor positioning
│   Compiler     │
│   (Sonnet)     │
└───────┬────────┘
        │ research-output.yaml
        ▼
┌────────────────┐
│   Content      │ ── draft content optimised for target platform
│   Writer       │◄─┐
│   (Sonnet)     │  │
└───────┬────────┘  │
        │           │ revision notes (max 2 rounds)
        ▼           │
┌────────────────┐  │
│    Editor      │──┘
│   (Sonnet)     │
└───────┬────────┘
        │ editor-review.yaml
        ▼
   Final Content
  (multi-platform)
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Brief Analyser** | Haiku | Raw brief | `specs/brief-analysis.yaml` | Parse brief, extract audience, tone, keywords, content type |
| **Research Compiler** | Sonnet | Brief analysis + knowledge base | `specs/research-output.yaml` | Gather data, statistics, angles, brand voice check |
| **Content Writer** | Sonnet | Brief analysis + research | `specs/content-output.yaml` | Write content following brand guidelines for target platform |
| **Editor** | Sonnet | All previous outputs | `specs/editor-review.yaml` | Review brand consistency, tone, SEO, readability, suggest edits |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines the complete deliverable after the revision cycle.

## Usage

```bash
# Run the full pipeline on a content brief
claude-code --agent agents/orchestrator.md \
  --input brief.txt \
  --output output/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/brief-analyser.md \
  --input brief.txt \
  --output brief-analysis.yaml
```

## Revision Loop

The pipeline includes a writer–editor feedback cycle:
1. Writer produces draft content
2. Editor reviews against brand voice, SEO, readability, factual accuracy
3. If `verdict: revise` — editor's notes go back to the writer (max 2 rounds)
4. If `verdict: pass` — content is finalised
5. If `verdict: reject` — escalate to human with editor's concerns

## Multi-Platform Output

The writer generates content optimised for the specified platform:
- **Blog** — full-length article with headings, meta description, SEO keywords
- **LinkedIn** — professional post with hook, body, CTA
- **Twitter/X** — thread or single post within character limits
- **Email** — subject line, preview text, body, CTA button text

## Customisation

- `specs/` — Modify output schemas to match your content model
- `.claude/agents/` — Adjust system prompts, tone, brand rules
- `knowledge-base/brand/` — Add your brand voice and style guides
- `knowledge-base/templates/` — Platform-specific content templates
- `config.yaml` — Pipeline settings (models, tone, SEO, platforms)

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet recommended for most agents, Haiku for brief analysis)

## Licence

MIT
