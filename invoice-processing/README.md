# Invoice & Expense Processing Agent Template

A multi-agent workflow for extracting, validating, and approving invoices and expense claims using Claude Code. Each sub-agent specialises in one step of the pipeline, producing structured YAML output that feeds the next stage. A human review gate ensures nothing is approved without oversight.

## Use Case

Finance teams processing 100+ invoices per week. Automates data extraction, policy validation, anomaly detection, and approval routing — replacing manual review that costs ~$65/hr in finance staff time.

## Architecture

```
Incoming Invoice / Expense Claim
              │
              ▼
     ┌─────────────────┐
     │    Extractor     │ ── vendor, amount, date, line items, VAT, currency
     │  Sub-Agent (H)   │
     └────────┬────────┘
              │ extractor-output.yaml
              ▼
     ┌─────────────────┐
     │    Validator     │ ── policy checks, GL codes, duplicate detection
     │  Sub-Agent (H)   │
     └────────┬────────┘
              │ validator-output.yaml
              ▼
     ┌─────────────────┐
     │ Anomaly Detector │ ── suspicious patterns, fraud indicators
     │  Sub-Agent (S)   │
     └────────┬────────┘
              │ anomaly-output.yaml
              ▼
     ┌─────────────────┐
     │    Approver      │ ── recommendation, routing, journal entry
     │  Sub-Agent (S)   │
     └────────┬────────┘
              │ approver-output.yaml
              ▼
        ┌──────────┐
        │  HUMAN   │ ── approve, query, or reject
        │  REVIEW  │
        └──────────┘
              │
              ▼
     Approved / Rejected
```

`(H)` = Haiku · `(S)` = Sonnet

## Sub-Agents

| Agent | Input | Output Spec | Purpose |
|-------|-------|-------------|---------|
| **Extractor** | Raw invoice/receipt text | `specs/extractor-output.yaml` | Parse and extract structured fields |
| **Validator** | Extractor output + policies | `specs/validator-output.yaml` | Check against expense policies, GL codes, duplicates |
| **Anomaly Detector** | Extractor + Validator output | `specs/anomaly-output.yaml` | Flag suspicious patterns and fraud indicators |
| **Approver** | All previous outputs | `specs/approver-output.yaml` | Generate approval recommendation and journal entry |

## Output Specs

Each sub-agent has a YAML spec in `specs/` that defines:
- Required fields and their types
- Allowed values (enums)
- Validation rules
- The contract between agents

The final output spec (`specs/final-output.yaml`) defines what the orchestrator produces after human approval.

## Key Features

- **Multi-currency support** — automatic conversion with configurable base currency
- **VAT/tax extraction** — handles standard, reduced, and zero-rated VAT
- **Duplicate invoice detection** — flags matching vendor + amount + date combinations
- **Approval routing** — routes to correct approver based on amount thresholds
- **GL code suggestion** — maps line items to general ledger codes
- **Fraud indicators** — flags unusual patterns and policy edge cases

## Usage

```bash
# Run the full pipeline on an invoice
claude-code --agent agents/orchestrator.md \
  --input invoice.txt \
  --output response/

# Run a single sub-agent (e.g. for testing)
claude-code --agent agents/extractor.md \
  --input invoice.txt \
  --output extractor-output.yaml
```

## Human Review Gate

The pipeline pauses after the Approver sub-agent. The human sees:
- Original invoice/expense claim
- Extracted data summary
- Validation results and any policy violations
- Anomaly flags (if any)
- Approval recommendation with suggested approver

Actions: **Approve** (mark as approved), **Query** (request more information), **Reject** (with reason), **Escalate** (route to senior finance).

## Customisation

- `specs/` — Modify output schemas to match your accounting system
- `agents/` — Adjust extraction rules, policy checks, anomaly thresholds
- `knowledge-base/` — Add your expense policies, vendor lists, GL codes
- `config.yaml` — Pipeline settings (currency, VAT rate, approval thresholds)

## Requirements

- Claude Code CLI
- Access to Claude API (Haiku for extraction/validation, Sonnet for anomaly detection/approval)

## Licence

MIT
