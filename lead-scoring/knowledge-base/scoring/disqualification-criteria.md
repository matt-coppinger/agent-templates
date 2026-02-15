# Disqualification Criteria

## Overview

Some leads should be disqualified regardless of their score. Check these criteria BEFORE applying score-based qualification thresholds.

## Automatic Disqualification

### 1. Competitor Domains
Leads from known competitor email domains are disqualified automatically. These should be flagged for the competitive intelligence team rather than sales.

**Current competitor domains** (maintained in `config.yaml`):
- competitor-a.com
- competitor-b.com

### 2. Students & Academics
Leads identifying as students, interns, or academics are not sales prospects. Indicators:
- Job title contains: student, intern, academic, researcher, professor, PhD candidate
- Email domain is a university (.ac.uk, .edu)
- Message references coursework, thesis, or academic research

**Action**: add to marketing newsletter list if they opt in; do not route to sales.

### 3. No Company Provided
If the lead provides no company name and their email domain doesn't map to a known organisation, disqualify. An individual with no company context cannot be scored against the ICP.

**Exception**: if the message content clearly describes a legitimate business need with enough context to infer a company, flag for manual review rather than auto-disqualifying.

### 4. Personal Email for Enterprise Tier
Leads using personal email addresses (Gmail, Yahoo, Hotmail, Outlook, iCloud, ProtonMail) who appear to represent enterprise-tier companies are suspicious. A VP at a 1,000-person company wouldn't typically use a Gmail address for vendor enquiries.

**Rule**: if estimated company size is 500+ AND email is from a personal domain, disqualify with a note to verify via LinkedIn or company website before re-engaging.

**Note**: personal email is acceptable for SMB and early-stage mid-market leads.

## Soft Disqualification (Human Review)

These don't auto-disqualify but should be flagged:

### 5. Geographic Mismatch
Lead is from a region you don't serve. Flag for review — they may have offices in served regions.

### 6. Unrealistic Expectations
Message indicates expectations far beyond product capability or budget far below minimum deal size. Flag for review.

### 7. Duplicate Lead
Same email or company submitted within the last 30 days. Flag as potential duplicate for the lead owner to merge.

## Disqualification Output

When disqualifying, always record:
- **Criterion matched**: which specific rule triggered disqualification
- **Evidence**: the data point that matched (e.g. "email domain: competitor-a.com")
- **Recommended action**: full exclusion, marketing list only, or re-engage after verification
