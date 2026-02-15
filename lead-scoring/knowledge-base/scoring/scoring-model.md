# Lead Scoring Model

## Overview

Leads are scored across four dimensions with a maximum total of 100 points. Each dimension captures a different aspect of lead quality and readiness to buy.

## Dimension 1: Firmographic Fit (0–30 points)

How well does the lead's company match our Ideal Customer Profile?

| Sub-Criterion | Points | Scoring Guide |
|---------------|--------|---------------|
| Company size match | 0–10 | 10: ideal ICP size, 7: acceptable range, 4: adjacent, 0: no company or far outside ICP |
| Industry alignment | 0–8 | 8: target industry, 5: adjacent/related, 2: neutral, 0: poor fit |
| Revenue band | 0–7 | 7: ideal revenue range, 4: acceptable, 2: unclear/estimated, 0: clearly outside range |
| Geography | 0–5 | 5: primary market, 3: secondary market, 1: tertiary, 0: unsupported region |

## Dimension 2: Behavioural Signals (0–25 points)

What actions has the lead taken that indicate engagement?

| Sub-Criterion | Points | Scoring Guide |
|---------------|--------|---------------|
| Source channel quality | 0–10 | 10: demo request, 8: referral, 6: content download, 4: webinar, 2: cold form, 0: unknown |
| Engagement depth | 0–8 | 8: multiple touchpoints, 5: single high-value action, 3: single low-value action, 0: passive |
| Content relevance | 0–7 | 7: product-specific content, 5: solution-area content, 3: general industry, 0: irrelevant/none |

## Dimension 3: Intent Signals (0–25 points)

What does the lead's communication reveal about buying intent?

| Sub-Criterion | Points | Scoring Guide |
|---------------|--------|---------------|
| Buying language | 0–8 | 8: "budget approved", "shortlisting vendors", 5: "evaluating", "looking for", 2: "interested in learning", 0: no buying language |
| Timeline indicators | 0–7 | 7: "this month/quarter", 5: "next quarter", 3: "this year", 1: "sometime", 0: no timeline |
| Pain point specificity | 0–5 | 5: specific named problem, 3: general pain, 1: vague dissatisfaction, 0: none stated |
| Decision authority | 0–5 | 5: C-suite/VP with budget, 3: manager evaluating, 1: individual contributor, 0: unclear |

## Dimension 4: Timing & Urgency (0–20 points)

How urgently does the lead need a solution?

| Sub-Criterion | Points | Scoring Guide |
|---------------|--------|---------------|
| Stated timeline | 0–7 | 7: "ASAP"/"this week", 5: "this quarter", 3: "this year", 1: "eventually", 0: none |
| Budget cycle alignment | 0–5 | 5: budget approved, 3: in planning cycle, 1: no budget discussion, 0: stated no budget |
| Competitive pressure | 0–4 | 4: actively comparing named vendors, 2: mentioned alternatives, 0: no competitive signals |
| Urgency language | 0–4 | 4: "urgent", "ASAP", "as soon as possible", 2: "soon", "when you can", 0: no urgency |

## Scoring Notes

- When data is missing for a sub-criterion, score at the midpoint of the range
- Round each sub-criterion to the nearest integer
- Total score = sum of all four dimension scores
- Document which sub-criteria contributed to each score
