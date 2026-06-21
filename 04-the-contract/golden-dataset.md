# Golden Dataset & Reliability Contract

## Golden Dataset Spec

| # | Input | Expected Output | Edge Case? | Judge Type |
|---|-------|----------------|-----------|-----------|
| 1 |Customer last invested 45 days ago, previously rolled over T-Bills every 14 days consistently for 6 months | | N | rule |
| 2 |Customer made first T-Bill purchase 5 days ago, no prior history | | Y | rule|
| 3 |Customer's contact frequency is normal but transaction value has dropped 70% over last 2 months (still investing, just much less) | Medium risk — "Still active, but investment value down 70% — may be moving funds elsewhere"| Y | LLM |
| 4 |Customer has irregular, seasonal investment pattern (e.g. invests heavily in December, quiet rest of year) and is currently in a quiet month | Should NOT be flagged high risk — "Quiet period consistent with historical seasonal pattern"| Y | LLM |
| 5 |Customer's last 3 transactions all failed/were abandoned mid-flow, but they kept retrying |Medium risk — "Active intent but hitting friction — investigate funding issues, not a disengagement signal" | Y |  LLM |

**Adversarial rows included:** 3 (rows 3, 4, and 5 — each designed to break a naive "days since last activity" rule by requiring the model to distinguish real disengagement from seasonal behavior, partial drop-off, or technical friction)__
**Coverage gaps identified by partner:** A naive version of this model would likely over-flag seasonal investors (row 4) and under-flag customers who are still "active" but quietly reducing exposure (row 3) — both are false signals a simple recency-based rule would miss. My partner also flagged that we have no row testing a customer who churns silently with no failed transactions and no contact — the cleanest, hardest-to-detect churn case, where there's no friction signal at all to point to, just gradual disengagement.

## Confidence UX Design

**Approach:** Tiered confidence with a human-in-loop trigger at the low end — the relationship manager should never act purely on a number without context, especially given regulatory sensitivity around customer communications.

**High confidence (>90%):** Clear, unambiguous pattern break (e.g. row 1) — surfaced directly as an actionable flag with the suggested reason, no human review required before the RM sees it.
**Medium confidence (70-90%):** Ambiguous cases (e.g. rows 3 and 5) — flagged but visually distinguished as "needs review," with the AI's reasoning shown so the RM can quickly judge whether to act, rather than the system presenting it as settled fact.
**Low confidence (<70%):** Seasonal or insufficient-history cases (e.g. rows 2 and 4) — not surfaced as a churn flag at all by default, but logged quietly so a human (or future model iteration) could review the borderline call later without spamming the RM with low-value flags.

**User control surface:** The RM should be able to dismiss a flag with a one-tap reason ("seasonal," "already contacted," "false positive") — this dismissal becomes our Correction Loop signal, feeding back into the model's future scoring rather than disappearing into nothing, which is exactly the gap we identified as currently missing in our Correction Loop today.

## Reliability Contract

| Metric | Target | Measurement | Alert Threshold |
|--------|--------|-------------|-----------------|
| Accuracy | ≥85% agreement with RM judgment on flagged cases|Weekly sample review of flagged vs. RM-confirmed churn risk |Below 75% triggers model review |
| Hallucination rate | <2% of explanations citing data not actually in the customer's record| Manual audit of explanation text against source data, sampled weekly| Above 5% halts auto-surfacing, reverts to human-only review|
| Latency (p95) | <3 seconds per customer risk score generation|Logged at API response level | Above 8 seconds triggers infra review|
| Drift velocity |<10% month-over-month shift in flag rate without a corresponding real change in customer behavior patterns | Monthly comparison of flag volume against macro investment activity trends| Above 15% unexplained shift triggers retraining review |

## HITL Architecture
<!-- When does a human step in? What's the escalation path? --> No churn flag is ever auto-actioned — every flag is a recommendation surfaced to a relationship manager, never an automatic customer-facing message or action. High-confidence flags still require RM acknowledgment before any outreach happens; medium-confidence flags require RM judgment before being acted on at all. Escalation path: if hallucination rate or drift velocity crosses its alert threshold, the system reverts to RM-only manual review (no AI flags surfaced) until a model review is completed and signed off internally — never silently continuing to serve degraded output.
 
## Red-Team Findings
*What failure mode did your partner find that you missed?* My partner pointed out the silent churn case — a customer with no failed transactions, no support contact, and no obvious friction, who simply stops investing gradually with no triggering event at all. Every row in my golden dataset assumes there's some signal to react to (a drop, a gap, a failed transaction). The hardest real-world case — someone who just quietly loses interest with zero anomalous behavior to flag — has no row testing it, and I don't have a clear answer yet for how the model would even attempt to catch that case versus a genuinely satisfied, low-activity long-term holder.


