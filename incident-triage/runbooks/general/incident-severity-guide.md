# Incident Severity Guide

## P1 — Critical
- Complete service outage
- Data loss or breach
- All users affected
- Revenue loss > £10,000/hour
- **Response time:** Immediately, all hands
- **SLA:** 15 min acknowledgement, 1 hour update cadence

## P2 — Major
- Significant degradation (>10% error rate)
- Subset of users affected
- Workaround may exist
- Revenue impact possible
- **Response time:** Within 30 minutes
- **SLA:** 30 min acknowledgement, 2 hour update cadence

## P3 — Minor
- Limited impact (<10% error rate)
- Workaround available
- Single feature or component affected
- **Response time:** Within 4 hours
- **SLA:** 4 hour acknowledgement, daily updates

## P4 — Low
- Cosmetic or edge case
- No user-facing impact
- **Response time:** Next business day
- **SLA:** 24 hour acknowledgement

## Escalation Triggers
- Any P1 automatically pages on-call lead
- P2 with revenue impact escalates to engineering director
- Any data breach escalates to security team + legal
- SLA breach risk escalates to customer success
