# Knowledge Base Q&A Agent Template

A RAG-powered multi-agent pipeline for answering questions from company documentation, FAQs, and product guides. Designed for customer service teams and internal support agents handling high-volume queries (300+/week). Each sub-agent specialises in one stage of the retrieval-augmented generation pipeline, producing structured YAML output that feeds the next stage.

## Architecture

```
Customer Question
      │
      ▼
┌────────────────┐
│ Query Analyser  │ ── intent, topic area, clarification needed?
│   Sub-Agent     │
└───────┬────────┘
        │ query-analysis-output.yaml
        ▼
┌────────────────┐
│   Retriever     │ ── search knowledge base, rank passages
│   Sub-Agent     │
└───────┬────────┘
        │ retrieval-output.yaml
        │
        ├── No relevant results? ──▶ "No answer found" path
        │
        ▼
┌────────────────┐
│  Synthesiser    │ ── generate answer with citations
│   Sub-Agent     │
└───────┬────────┘
        │ synthesis-output.yaml
        ▼
┌────────────────┐
│   Verifier      │ ── hallucination check, confidence score
│   Sub-Agent     │
└───────┬────────┘
        │ verification-output.yaml
        │
        ├── High confidence ──▶ Return answer
        ├── Low confidence  ──▶ Flag for human review
        └── Hallucination   ──▶ Reject & escalate
```

## Sub-Agents

| Agent | Model | Input | Output Spec | Purpose |
|-------|-------|-------|-------------|---------|
| **Query Analyser** | Haiku | Raw question | `specs/query-analysis-output.yaml` | Parse intent, identify topic, detect clarification needs |
| **Retriever** | Haiku | Analyser output + knowledge base | `specs/retrieval-output.yaml` | Search docs, rank by relevance, extract passages |
| **Synthesiser** | Sonnet | Analyser + Retriever output | `specs/synthesis-output.yaml` | Generate coherent answer with citations |
| **Verifier** | Sonnet | All previous outputs | `specs/verification-output.yaml` | Check accuracy, flag hallucination, assess confidence |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines the complete pipeline response.

## Usage

```bash
# Run the full pipeline on a customer question
claude-code --agent agents/orchestrator.md \
  --input question.txt \
  --output response/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/query-analyser.md \
  --input question.txt \
  --output query-analysis-output.yaml
```

## Key Features

### Hallucination Detection
The Verifier sub-agent checks every claim in the synthesised answer against the retrieved passages. Claims not grounded in source material are flagged, and the answer is rejected if hallucination risk is high.

### No Answer Found Path
When the Retriever finds no relevant documents (all similarity scores below threshold), the pipeline short-circuits and returns a structured "no answer found" response with suggested next steps (e.g. contact support, rephrase question).

### Confidence-Based Routing
- **High confidence (≥0.8):** Return answer directly
- **Medium confidence (0.5–0.8):** Return answer with caveat, flag for review
- **Low confidence (<0.5):** Escalate to human agent

### Citation Tracking
Every claim in the final answer includes a citation to the source document and passage, enabling verification and trust.

## Customisation

- `specs/` — Modify output schemas to match your data model
- `.claude/agents/` — Adjust sub-agent prompts, retrieval strategy, verification rules
- `knowledge-base/` — Add your company docs, FAQs, product guides, policies
- `config.yaml` — Pipeline settings (confidence thresholds, max sources, language)

## ROI Estimate

At 300 queries/week and £35/hr staff cost, automating even 60% of queries saves approximately:
- **180 queries/week** handled without human intervention
- **~45 staff hours/week** saved (assuming 15 min per query)
- **~£1,575/week** or **£81,900/year** in direct cost savings

## Requirements

- Claude Code CLI
- Access to Claude API (Sonnet for synthesiser/verifier, Haiku for analyser/retriever)

## Licence

MIT
