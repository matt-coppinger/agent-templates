# {RUNBOOK_TITLE}

> **Service:** {SERVICE_NAME}
> **Owner:** {TEAM_NAME}
> **Last updated:** {DATE}
> **Severity:** {P1/P2/P3/P4}

## Overview

{What this runbook covers and when to use it.}

## Prerequisites

- {Access requirements}
- {Tools needed}
- {Permissions required}

## Detection

{How this issue is typically detected — alerts, monitoring, customer reports.}

**Key Metrics**

| Metric | Normal Range | Alert Threshold |
|--------|-------------|-----------------|
| {metric} | {range} | {threshold} |

## Diagnosis

### Step 1: {First diagnostic step}

```bash
{command to run}
```

**Expected output:** {what you should see}

**If abnormal:** {what to do next}

### Step 2: {Second diagnostic step}

```bash
{command to run}
```

## Resolution

### Option A: {Primary fix}

1. {Step 1}
2. {Step 2}
3. {Step 3}

```bash
{commands}
```

### Option B: {Alternative fix}

{When to use this alternative and the steps.}

## Rollback

{How to undo the changes if the fix makes things worse.}

```bash
{rollback commands}
```

## Verification

{How to confirm the issue is resolved.}

- [ ] {Check 1}
- [ ] {Check 2}
- [ ] {Check 3}

## Escalation

| Condition | Escalate To | Contact |
|-----------|-------------|---------|
| {condition} | {team/person} | {contact method} |

## Post-Incident

- [ ] Update this runbook with lessons learnt
- [ ] File post-mortem if P1/P2
- [ ] Update monitoring/alerting if gaps found

## Changelog

| Date | Author | Changes |
|------|--------|---------|
| {date} | {author} | {summary} |
