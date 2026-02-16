# Agent Templates

Open source agent templates for [Claude Code](https://code.claude.com). Each template implements a real enterprise use case using multiple sub-agents with structured YAML output specs, human review gates, and full audit trails.

## Philosophy

- **Partial automation** — agents do the work, humans approve it
- **YAML output specs** — every sub-agent produces consistent, validated output
- **Auditable** — complete pipeline output saved to disk for compliance and cost tracking
- **Customisable** — swap knowledge bases, adjust tone, change models, add policies

## Templates

| Template | Sub-Agents | Status |
|----------|-----------|--------|
| [Customer Service](./customer-service/) | Classifier → Researcher → Drafter → Reviewer | ✅ Ready |
| [Incident Triage](./incident-triage/) | Classifier → Investigator → Responder → Reviewer | ✅ Ready |
| [Lead Scoring](./lead-scoring/) | Enricher → Scorer → Qualifier → Router | ✅ Ready |
| [Knowledge Base Q&A](./knowledge-base-qa/) | Query Analyser → Retriever → Synthesiser → Verifier | ✅ Ready |
| [Sentiment Routing](./sentiment-routing/) | Emotion Detector → Context Assessor → Priority Scorer → Router | ✅ Ready |
| [Code Review](./code-review/) | Diff Analyser → Bug Scanner → Style Checker → Review Composer | ✅ Ready |
| [Invoice Processing](./invoice-processing/) | Extractor → Validator → Anomaly Detector → Approver | ✅ Ready |
| [CV Screening](./cv-screening/) | Parser → Matcher → Assessor → Ranker | ✅ Ready |
| [HR Policy Q&A](./hr-policy-qa/) | Intent Classifier → Policy Retriever → Response Generator → Compliance Checker | ✅ Ready |
| [Contract Review](./contract-review/) | Clause Extractor → Risk Assessor → Comparator → Summary Writer | ✅ Ready |
| [Content Creation](./content-creation/) | Brief Analyser → Research Compiler → Content Writer → Editor | ✅ Ready |
| [Doc Generation](./doc-generation/) | Code Analyser → Structure Planner → Doc Writer → Quality Reviewer | ✅ Ready |
| [Quality Assurance](./quality-assurance/) | Data Parser → Pattern Detector → Root Cause Analyser → Report Generator | ✅ Ready |
| [Regulatory Monitoring](./regulatory-monitoring/) | Feed Scanner → Change Analyser → Impact Assessor → Briefing Writer | ✅ Ready |
| [Due Diligence](./due-diligence/) | Document Indexer → Risk Extractor → Cross-Referencer → Report Writer | ✅ Ready |
| [PRD Drafting](./prd-drafting/) | Input Parser → Research Enricher → Spec Writer → Reviewer | ✅ Ready |
| [Financial Forecasting](./financial-forecasting/) | Data Ingester → Trend Analyser → Forecaster → Narrative Writer | ✅ Ready |

## How It Works

Each template is a self-contained Claude Code project with:

```
template-name/
├── CLAUDE.md                    # Orchestrator instructions
├── config.yaml                  # Pipeline settings (models, tone, thresholds)
├── .claude/agents/              # Sub-agent definitions (Claude Code format)
│   ├── agent-1.md
│   ├── agent-2.md
│   └── ...
├── specs/                       # YAML output schemas per stage
│   ├── stage-1-output.yaml
│   ├── stage-2-output.yaml
│   └── final-output.yaml
├── knowledge-base/              # Your company docs (add your own)
├── examples/                    # Sample inputs for testing
└── output/                      # Audit trail (gitignored)
```

1. **Launch Claude Code** in the template directory
2. **Give it a task** (e.g. "Process the ticket in examples/sample-ticket.txt")
3. **Sub-agents run in sequence**, each producing YAML conforming to its spec
4. **Human review gate** — you approve, edit, reject, or escalate
5. **Audit trail** — every stage's output saved to `output/{id}/`

## Quick Start

```bash
# Clone the repo
git clone https://github.com/matt-coppinger/agent-templates.git
cd agent-templates/customer-service

# Add your knowledge base docs
cp your-docs/* knowledge-base/

# Edit config
vi config.yaml

# Run with Claude Code
claude
```

Then prompt:

```
Process the customer ticket in examples/sample-ticket.txt through the full pipeline.
```

## Requirements

- [Claude Code CLI](https://code.claude.com) installed and authenticated
- Claude API access (Sonnet recommended for most sub-agents, Haiku for classification)

## Design Principles

**Consistent output via YAML specs** — Each sub-agent has a spec file defining required fields, types, allowed values, and a complete example. The agent reads the spec and produces conforming output. No ambiguity.

**Sub-agents stay in their lane** — The classifier doesn't write responses. The researcher doesn't make policy decisions. The drafter doesn't quality-check itself. Separation of concerns.

**Human-in-the-loop by default** — Every template pauses for human approval before taking action. The reviewer sub-agent provides a summary so humans can make fast, informed decisions.

**Full audit trail** — Every pipeline run writes each stage's output to disk. Track what was classified, what was found, what was drafted, what was reviewed, and what the human decided. Essential for regulated industries.

## Contributing

PRs welcome. If you build a template for a new use case, follow the existing structure and include:
- Sub-agents in `.claude/agents/` with proper frontmatter
- YAML output specs in `specs/`
- A sample input in `examples/`
- A `README.md` explaining the pipeline
- A `config.yaml` for customisation

## Licence

MIT
