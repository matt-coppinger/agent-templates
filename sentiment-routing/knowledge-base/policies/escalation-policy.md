# Escalation Policy

## Automatic Escalation Triggers

The following conditions trigger automatic escalation without waiting for standard routing:

### P1 — Immediate Escalation
- **Safety threats:** Any reference to self-harm, threats of violence, or personal safety concerns → Safety & Legal team immediately
- **Legal threats:** Mention of lawyers, solicitors, legal proceedings, or regulatory bodies (Ofcom, FCA, ICO, Trading Standards) → Safety & Legal team immediately
- **Regulatory complaints:** GDPR requests, data protection complaints, formal regulatory submissions → Safety & Legal team within 15 minutes

### P2 — Urgent Escalation
- **VIP customer with anger intensity ≥ 0.7:** Route to team senior or manager
- **Churn risk ≥ 0.7:** Override to Retention team regardless of issue category
- **Repeat contact (3+ times) about unresolved issue:** Escalate to team senior
- **Service outage affecting multiple customers:** Route to Engineering On-Call

## Escalation Path

```
Agent → Senior Agent → Team Lead → Department Manager → Head of Customer Success → COO
```

Each escalation level has 30 minutes to acknowledge before automatic further escalation.

## Repeat Contact Rules

- **2nd contact** about same issue: Flag for awareness, assign to experienced agent
- **3rd contact** about same issue: Escalate to team senior, mandatory same-agent assignment
- **4th+ contact** about same issue: Escalate to team manager, proactive outreach required within 2 hours

## VIP Escalation

VIP customers (see config.yaml for thresholds) receive:
- Minimum handling by senior agent or above
- Manager notification for any P1 or P2 ticket
- Proactive follow-up within 24 hours of resolution
- Account review triggered after 2+ escalations in 90 days

## De-escalation Authority

| Level | Authority |
|-------|-----------|
| Agent | Apology, expedited handling, waive minor fees (< £25) |
| Senior Agent | Goodwill credit up to 1 month, extended deadline |
| Team Lead | Goodwill credit up to 2 months, custom resolution |
| Manager | Goodwill credit up to 3 months, custom pricing, feature unlock |
| Head of CS | Full commercial authority, contract renegotiation |

## Documentation Requirements

All escalations must be documented with:
1. Reason for escalation
2. Actions taken before escalation
3. Customer's current emotional state
4. Recommended next steps
5. Timeline of all contacts related to this issue
