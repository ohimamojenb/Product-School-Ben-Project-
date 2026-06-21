# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | _2_/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | _2_/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | _3_/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | _1_/5 |

### Correction Loop - _2_/5
**What you capture today:**
We're logging order errors, failed transactions, and support escalations and through MoEngage, we're already closing part of the loop on this. When a transaction fails, that event triggers a notification back to the customer, prompting them to retry or get support. That's a real, live mechanism, not just passive logging.
**How it compounds:**
Right now the loop closes at the customer level, they get nudged to fix their own failure. What's still missing is closing it at the product level: using the pattern of failures (e.g. "60% of failures happen at the funding step") to drive product or UX changes. The customer-facing trigger is solid; the product-learning side is the next layer to add.

### Preference Loop - _2_/5
**What you capture today:**
We have rich underlying data, full holdings and transaction history per customer. That's the hard part already solved. What's missing is using that data to shape the next interaction inside the product itself.
**How it compounds:**
Because the data foundation is strong, this is a fast loop to improve. A customer who's rolled over three T-Bills getting a renewal prompt instead of a blank screen is a near-term, achievable win, not a long-term build.

### Domain Context Loop - _3_/5
**What you capture today:**
This is genuinely our best-positioned loop. The structural advantage is real and rare Capital sits inside a Group with Asset Management and Merchant Bank, and the Unified Wealth Dashboard programme is already underway to formalize it. Most competitors don't have this option available to them at all.
**How it compounds:**
Once live, this becomes very hard to replicate, a fixed income maturity prompting an Asset Management suggestion, or salary flow surfacing a Capital prompt. We're early, but we're building on the strongest possible foundation.

### Network Loop - _1_/5
**What you capture today:**
Nothing live yet — but this is the most common loop to be early on across fintech generally, and it's the one most deliberately sequenced for later phases rather than overlooked.
**How it compounds:**
A simple referral mechanic is a well-understood, low-risk first move whenever we're ready to prioritize it.

**Total Flywheel Score: _9_/20**
**Weakest Loop:** Preference and Network are tied at the floor (1/5) — but Preference is the one I'd prioritize first, since it has the clearest path to quick impact given how strong our underlying data already is.
**Fix for weakest loop:** A single rule-based renewal prompt using existing transaction data, no new infrastructure or AI model required. Given the strength of our data foundation, this is genuinely close at hand, not a distant roadmap item.

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:** Stanbic IBTC Investments + Meristem + CardinalStone Vector
**Vector:** All three offer multi-asset investment platforms (equities, fixed income, mutual funds) through both web and mobile — directly mirroring Capital's proposition. CardinalStone and Meristem specifically serve the same SEC-registered, mid-to-high net worth retail and HNI investor segment that Capital is targeting. They also have longer track records and established trust with that segment. Time-to-threat: 0–3 months (all already live) % of 
**Time-to-threat:** 0–3 months (all already live) of %
**% of value at risk:** 50%

### 2. Vertical Competitor
**Attacker:** Bamboo + Chaka + Afrinvest
**Vector:** Bamboo and Chaka win on UX and onboarding friction. Afrinvest brings research and stockbroking credibility. This is the segment most likely to convert dissatisfied users in the near term, since their value proposition is the in-app experience, exactly where we're earliest in our build-out.
**Time-to-threat:** 3–6 months % 
**% of value at risk:** 35%

### 3. Adjacent Expansion
**Attacker:** Paystack / MoMo / Moniepoint / OPay
**Vector:** They already own the payment relationship and wallet habit. Adding yield/investment is a single feature ship for them, with zero acquisition cost. OPay specifically already runs OWealth, making this an extension of something live rather than a hypothetical.
**Time-to-threat:** 6–12 months % 
**% of value at risk:** 25%

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** MTN MoMo / Moniepoint / OPay
**Attack vector (target the weakest loop):** Preference and Network Loop — it's the most visibly felt by users day-to-day, and the one with the clearest near-term fix available to us once prioritized.
**Weeks 1-4 - what they ship:** OPay extends OWealth to include T-Bills and money market funds directly in the wallet. No new KYC needed, BVN/NIN already on file. Yield sits next to spendable balance in the same screen, making the offer feel immediate and tailored.
**Weeks 5-8 - how they poach users:** Referral push: "Invite a friend, you both earn ₦1,000 + bonus yield." Idle-balance nudges target users directly: "Your balance has been sitting for 5 days, earn 18% instead." This plays directly into the Preference gap we've identified, and is the clearest argument for prioritizing the renewal-prompt fix soon.
**Weeks 9-12 - why users don't come back:** Auto-reinvestment by default, unified view of spending + investment in one dashboard. A user who tried Capital and found the funding flow slower, with no follow-up nudge bringing them back, simply moves on, underscoring why even a simple win-back mechanism would have outsized value relative to its build cost.


**Your defense:**
Against OPay's wallet-embedded T-Bills, our defense is SEC-licensed, DCS exchange-settled trust — the one thing they structurally cannot replicate quickly. This is live today and remains our core moat.
Against idle-balance personalised nudges, our defense is a rule-based renewal prompt using existing transaction data. We have a strong foundation in place already, so this is quick to build.
Against referral-driven acquisition, our defense is a basic referral/invite mechanic. This is a clear, low-risk next step once prioritized.
Against the unified wallet view versus our currently fragmented Capital experience, our defense is the Unified Wealth Dashboard. Phase 1 is underway, and this remains our strongest long-term differentiator.

