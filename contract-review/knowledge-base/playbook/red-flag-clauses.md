# Red Flag Clauses — Always Escalate to Senior Review

These clause patterns always require escalation to senior counsel, regardless of overall contract risk. If any of these are detected, flag `is_red_flag: true` and `escalation_required: true`.

---

## 1. Uncapped Liability

**Pattern:** No monetary cap on one or both parties' liability, or cap set at a nominal amount.

**Why it's a red flag:** Unlimited financial exposure. Even "standard" uncapped liability for IP indemnity should be scrutinised.

**Look for:** "unlimited liability", absence of any cap clause, cap below 50% of contract value.

---

## 2. One-Sided Indemnity (Uncapped)

**Pattern:** Only one party provides indemnification, or indemnity is uncapped and not subject to the liability limitation.

**Why it's a red flag:** Disproportionate risk allocation. Common in vendor-drafted contracts.

**Look for:** Indemnity clauses that lack reciprocity, indemnity expressly carved out from liability cap.

---

## 3. Broad IP Assignment

**Pattern:** All intellectual property created during the engagement (including pre-existing IP, background IP, or general know-how) is assigned to the counterparty.

**Why it's a red flag:** Could transfer valuable pre-existing assets. "Work made for hire" language (US concept) in a UK contract is also a red flag.

**Look for:** "all IP", "work product", "work made for hire", assignment of background IP, no licence-back provision.

---

## 4. Unilateral Variation

**Pattern:** One party may amend the terms by notice, by updating a website, or "at its sole discretion".

**Why it's a red flag:** Undermines contractual certainty. May be unenforceable but creates risk.

**Look for:** "may amend from time to time", "by publishing on our website", "at sole discretion".

---

## 5. Automatic Renewal Without Adequate Notice

**Pattern:** Contract auto-renews for successive terms with a very short or no opt-out window (e.g. 14 days' notice).

**Why it's a red flag:** Creates lock-in. May result in unintended multi-year commitments.

**Look for:** Auto-renewal with notice periods under 30 days, evergreen clauses with no exit mechanism.

---

## 6. Exclusive Jurisdiction in Foreign Territory

**Pattern:** Disputes governed by or subject to the exclusive jurisdiction of courts in a jurisdiction unfavourable or unfamiliar to our side.

**Why it's a red flag:** Enforcement difficulty, unfamiliar legal system, increased costs.

**Look for:** Governing law of a jurisdiction where we have no presence, mandatory arbitration in a distant forum.

---

## 7. Penalty Clauses / Excessive Liquidated Damages

**Pattern:** Liquidated damages that are disproportionate to the likely loss, or clauses that function as penalties.

**Why it's a red flag:** Penalty clauses are unenforceable under English law (Cavendish Square v Makdessi), but create dispute risk.

**Look for:** Fixed sums that bear no relation to actual loss, escalating penalties, "penalty" language.

---

## 8. Unrestricted Data Use

**Pattern:** Counterparty claims broad rights to use, share, or commercialise data provided under the contract.

**Why it's a red flag:** Data protection compliance risk (UK GDPR), competitive risk, potential regulatory exposure.

**Look for:** "may use data for any purpose", lack of data processing agreement, broad data sharing with affiliates/third parties.

---

## 9. Waiver of Statutory Rights

**Pattern:** Clauses purporting to waive statutory protections (e.g. Sale of Goods Act implied terms for consumers, TUPE rights).

**Why it's a red flag:** May be unenforceable and indicate bad-faith drafting.

**Look for:** "waives all statutory rights", exclusion of implied terms where not permitted, TUPE indemnities without proper protections.

---

## 10. No Termination for Convenience

**Pattern:** No right for either party (or only one party) to terminate without cause.

**Why it's a red flag:** Creates lock-in for the full term with no exit route.

**Look for:** Absence of termination for convenience, termination only for cause, termination subject to onerous conditions (e.g. payment of all remaining fees).

---

## 11. Non-Compete Beyond 12 Months

**Pattern:** Restrictive covenants (non-compete, non-solicitation) extending beyond 12 months or covering unreasonably broad geographic/activity scope.

**Why it's a red flag:** Likely unenforceable under English law but creates litigation risk and commercial constraint.

**Look for:** Non-compete periods over 12 months, worldwide scope, overly broad activity restrictions.

---

## 12. Guarantee / Parent Company Guarantee Without Limit

**Pattern:** Requirement for unlimited parent company or personal guarantee.

**Why it's a red flag:** Exposes the guarantor to uncapped liability for the subsidiary's obligations.

**Look for:** "unconditional guarantee", "on demand", guarantee not capped or time-limited.

---

## Escalation Process

When a red flag is detected:
1. Flag in the risk assessment output with `is_red_flag: true`
2. Set `escalation_required: true`
3. Include the specific red flag category and reason
4. The orchestrator will route to senior counsel for review
5. **Never** recommend acceptance of a red-flag clause without senior review
