# Cost Curve & Pricing Strategy

## Cost Model

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| KYC / Identity Verification (Prembly)| ₦225 – ₦375|Industry-average per-verification cost for BVN/NIN/CAC checks via providers like Prembly, amortized monthly assuming one verification per new user, spread across average customer lifetime |
| Market Data / Order Routing (NGX/Infoware) | ₦450 – ₦750|Estimated blended cost of live market data feed access and per-order routing fees, based on typical capital markets middleware pricing in Nigeria |
| Wallet Funding / Transfers (NIBSS/NIP) | ₦75 – ₦150|NIBSS NIP transfer fees typically range ₦10–₦50 per transaction; averaged across an estimated 2–3 funding transactions per user/month |
| Customer Engagement (MoEngage) |₦150 – ₦300 |Typical CDP/marketing automation pricing scales with monthly active users and message volume (push, email, SMS); mid-range estimate for a platform our size |
| Data / Storage (Azure) |₦150 |Confirmed — $100/month flat ÷ 250 users = $0.40/user, converted at ₦1,500/$1 |
| **Total AI COGS** |₦1,050 – ₦1,725 |Per user/month, based on industry-average estimates; actual figures require vendor contract confirmation |

## Cascading Strategy
<!-- Cheap model → frontier model routing logic --> Not applicable in the traditional AI sense  Capital has no AI inference layer today, so there's no cheap-model-to-frontier-model routing happening.
The closest equivalent concept that does exist in our build: MoEngage's rule-based triage, simple trigger-based notifications (failed transaction, idle balance) are handled by lightweight rule logic rather than anything resembling a "frontier model." If an AI layer were added later (e.g. ChurnGuard), this is where a triage model would sit, handling simple queries before escalating to a more expensive model.


**Triage model:** N/A today — would be a lightweight model handling simple classification (e.g., "is this customer at risk: yes/no") if AI were introduced
**Frontier model:** N/A today — would handle the more nuanced "why" explanation behind a risk flag
**Routing rule:** N/A — no AI routing exists in the current build
**Expected cascade ratio:** N/A

## Pricing Model

**Current pricing:** Capital does not charge customers a separate platform/subscription fee. Revenue comes from transaction-based mechanisms, fees or spreads embedded in T-Bills, Commercial Papers, FGN Bond purchases, and equities trading, consistent with standard capital markets brokerage economics, priced and settled in Naira.
**Proposed AI pricing:** Not applicable — no AI feature is live or monetized today. If a feature like ChurnGuard were introduced as an internal tool, it would not be customer-facing pricing at all; it would be an internal cost absorbed as part of platform operations, justified by improved retention rather than direct revenue.
**Model:** N/A — current revenue model is transaction/fee-based, not seat, usage, or outcome-based in the way this template assumes for an AI product.

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x |Storage moves from ₦150 to ₦450/user/month — meaningful at 250 users, but dilutes quickly as user base scales, since Azure's flat base cost doesn't scale linearly with users |Revisit storage architecture efficiency; at scale (5,000+ users), even a 3x increase becomes immaterial per-user |
| Heaviest segment doubles |NIBSS and NGX/Infoware per-transaction costs scale directly with this segment, increasing total COGS proportionally; margin impact depends on whether our transaction fee structure also scales with volume | Since revenue is also transaction-based, doubled volume should largely be margin-neutral or margin-positive, unlike a flat-fee AI cost structure would be|
| Model provider raises prices 50% |Direct hit to COGS on whichever line item is affected — Infoware/NGX is the largest cost line, so a 50% increase there has the biggest absolute impact |This is exactly the scenario covered in our Kill Switch Audit — for Infoware specifically, our direct NGX integration gives us real negotiating leverage; for NIBSS, we have no fallback and would need to absorb cost or evaluate fee pass-through to customers |

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):** Capital does not operate on a traditional SaaS revenue model today,  there is no subscription or seat fee. Revenue is transaction-based: fees and spreads embedded in T-Bills, Commercial Papers, FGN Savings Bonds, and equities trades. Revenue is directly tied to transaction volume and AUM, which means it's also directly exposed to churn, every customer who quietly stops investing (the gap our Preference Loop weakness leaves open) is lost revenue with no recurring floor underneath it.
**After (AI-enabled):** If a feature like ChurnGuard were introduced, flagging at-risk customers before they go fully dormant, the revenue model itself wouldn't change (still transaction-based), but the retention curve underneath it would. Fewer customers going silent means more renewed T-Bills, more reinvested CP maturities, and a higher average AUM per retained customer over time. The AI layer here doesn't create a new revenue line; it defends the existing one by reducing silent attrition before it shows up in the numbers.
**Net margin shift:** Minimal direct cost impact, ChurnGuard as scoped is a lightweight, rule-based-to-AI feature, not a heavy inference workload, so it doesn't meaningfully add to COGS (our Cost Model above shows no material AI cost today). The margin shift is on the revenue side, not the cost side: even a modest reduction in customer churn compounds directly into retained transaction fees and AUM, since we're not paying a SaaS-style cost to deliver this, we're paying a small operational cost to protect revenue that already exists but is currently leaking silently.
