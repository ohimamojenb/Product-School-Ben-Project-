# Compounding System Design

## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
|Correction (MoEngage failure trigger) |Failed transaction event |Customer notification prompting retry/support | N | active but not compounding — closes at customer level only, never feeds back into product decisions |
|Preference (transaction history) | Customer holdings and transaction history|Nothing — no personalised next-step surfaced | N | missing |
| Domain Context (cross-subsidiary data)|Capital, Asset Management, Merchant Bank activity within FSDH Group |Unified Wealth Dashboard (Phase 1, not yet live) | Y (once live)| broken — the structural input exists, but the output isn't connected yet|

**Broken loop identified by partner:** The Correction loop — my partner pointed out that we're treating "customer got notified" as if it closes the loop, but it doesn't. The loop only closes when the pattern of failures changes something on the product side. Right now we fix the customer's immediate problem and learn nothing as a business
**Fix plan:** Route failed-transaction data (which MoEngage already triggers on) into a weekly review — tag failure type and location in the flow, and feed the top recurring failure point into sprint prioritisation. This requires no new infrastructure, just a reporting habit change.

## Context Connectivity
<!-- How does knowledge flow across teams and domains? Where does it silo? --> Today, knowledge flows poorly across FSDH Group — Capital, Asset Management, and Merchant Bank each operate mostly siloed, with Digital Strategy acting as one of the few connective points, but informally rather than through any systematic mechanism. A customer's activity on Capital (a T-Bill maturity, a withdrawal pattern, a churn signal) doesn't naturally inform what Asset Management or Merchant Bank know about that same customer, even though they're legally one Group serving the same underlying base.
This is exactly the gap the Unified Wealth Dashboard programme is meant to close — but it's still Phase 1, and until it's live, the cross-subsidiary advantage we keep citing as our structural moat (Domain Context Loop) is more theoretical than operational. We have the organisational shape of a connected Group, but not yet the data pipes that make that shape useful. Most of what does cross between teams today happens through individual relationships and ad hoc requests — Digital Strategy pulling context from Capital for a Group Shared Services initiative, for example — rather than through any system designed to make that flow automatic.


## Governance Policy
(Forward-looking — no formal AI governance policy exists at FSDH/Capital today, beyond official sanctioning of Copilot as a tool. This represents what would need to be established before any AI feature like ChurnGuard could responsibly go live.)
**Scope:** Any AI feature would apply to Capital's customer-facing investment platform and internal relationship management tools only — explicitly excluding anything that generates customer-facing investment advice or executes transactions autonomously, given SEC oversight on what constitutes regulated investment advice.
**Autonomy boundaries:** AI can flag, score, and suggest — it cannot communicate directly with customers, cannot execute trades or transfers, and cannot make any decision that affects a customer's account without a human (relationship manager or compliance) in the loop.
**Escalation triggers:** Any AI output flagged as high-risk for hallucination, drift, or accuracy breach (per the Reliability Contract thresholds defined for ChurnGuard) automatically escalates to a human review queue. Any AI feature touching customer data must escalate to the Data Protection Officer and Compliance before launch, given NDPR obligations already governing how we handle BVN, NIN, and transaction data.
**Audit cadence:** Quarterly review of any live AI feature's outputs against its Reliability Contract metrics, reported to the same governance structure currently reviewing VAPT and risk acceptance items (ED Risk and Compliance, CISO).
**Regulatory exposure (EU AI Act / other):** EU AI Act doesn't directly apply since Capital operates purely within Nigeria, but the relevant domestic exposure is NDPR (data protection) and SEC rules on what constitutes regulated investment advice — any AI output that could be construed as a recommendation to buy/sell/hold a specific instrument risks crossing into licensed-advisor territory.

## Agent Topology
<!-- If using agents: what can each agent do? What can't it do? Who approves what? --> We don't have any AI agents live today — ChurnGuard as scoped is a single-purpose tool, not a multi-agent system: it takes customer transaction/contact history as input and produces a risk score plus a plain-English reason as output. There's no chaining, no agent calling another agent, no autonomous action.
If this grew into a multi-agent system in future, a plausible topology would be: one agent scores churn risk (the current ChurnGuard scope), a second agent drafts a suggested outreach message based on that score (similar to the WhatsApp follow-up draft concept we explored earlier), and a third agent (or a human) approves the message before it goes out. Each agent's role would stay narrow and bounded — no agent would be allowed to send a message directly to a customer; a human always approves the final action, consistent with the autonomy boundaries set above.


## Shadow AI Audit

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
|Microsoft Copilot |FSDH Group IT (officially sanctioned) |  L | keep |
|Claude (this tool) | Benjamin, individual use for drafting/strategy work| M | govern — useful and currently low-harm, but no formal policy exists on what customer or company data is appropriate to share with it |
| ChatGPT|Benjamin, individual use | M | govern — same reasoning as Claude; valuable for productivity but needs a data-handling guideline before broader team use |

**Total tools found:** 
**Tools after triage:** 3 (none recommended for outright kill — Copilot is already governed by being official; Claude and ChatGPT need governance, not elimination, since they're providing real value for drafting and strategic thinking)
**Estimated hidden spend:** Unknown — likely minimal in direct cost (personal/individual logins rather than enterprise contracts), but the real hidden cost is ungoverned exposure: company-sensitive data (PRDs, strategy documents, customer data references) potentially being shared with tools that have no FSDH-specific data handling agreement in place.
