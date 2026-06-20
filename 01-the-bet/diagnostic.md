# Three-Axis Vulnerability Diagnostic

## Product
<!-- Name the product you're diagnosing. Real product at your company — not a hypothetical. -->

**Product:** FSDH Capital — Digital Investment Platform (Mobile/Web)
**Your Role:** Product Manager, Digital Strategy

---

## Scores

### Contextual Moat — _2_/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:** I gave myself a 2 here, not higher. We have real depth — T-Bills, FGN Bonds, Commercial Papers, NGX Equities, all SEC-regulated, plus DCS for exchange-settled trust. That's not nothing. But depth isn't the same as lock-in. Honestly, if a user has one T-Bill position and Stanbic shows up with the same thing and a slicker app, they're gone in a weekend. Onboarding still has friction — BVN, CAC, NIN checks — and once someone's past that, there's nothing pulling them back in. No habit loop. I built the access, not the stickiness.

**Named attacker (from partner challenge):** Stanbic IBTC Investments — same multi-asset depth, stronger brand trust, larger existing customer base to convert.

---

### Data Advantage — _2_/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:** I pushed back on myself here, I almost scored this a 1, but that's not fair to what we've actually built. We run MoEngage, and we are personalizing engagement, segmented push, email, SMS based on behaviour and lifecycle stage. That's real signal, and we're acting on it. But I'm capping it at 2 because it's engagement-layer, not product-layer. MoEngage decides when you get pinged and what the message says, it doesn't change what you see inside the app. No recommendation engine, no adaptive nudges in-product, nothing compounding back into product decisions. Any competitor on Braze or Customer.io has the same capability. It's real, it's just shallow.

**Named attacker (from partner challenge):** Bamboo / Cardinal stone  — probably running similar engagement tooling, but their personalisation lives inside the product, not just in notifications.

---

### Platform Exposure — _2_/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:** This one worries me the most long-term. Our hero feature is frictionless access to T-Bills and money market instruments. MoMo or Moniepoint could ship that as a feature inside a wallet people already use daily,  zero acquisition cost for them. And our pivot speed is slow. We move in phases, compliance and business has to sign off, the Unified Wealth Dashboard is still Phase 1. If MoMo ships this in 90 days, we don't have a 90-day response ready.

**Named attacker (from partner challenge):** MTN MoMo, Opay, Moniepoint — they already own the wallet relationship and the transaction frequency. A yield feature is one build away for them.

---

## Top Vulnerability
<!-- One line: what's the single biggest strategic risk? --> I've got the regulatory and product breadth, plus shallow personalisation through MoEngage — but nothing compounding inside the product itself. That leaves me exposed on two sides at once: fintechs out-personalising me in-app, and payment platforms that can ship my hero feature natively without acquiring a single new user.

## Confidence Level
<!-- H / M / L — how confident are you in this bet after the diagnostic? --> My regulatory moat is real and hard to fake quickly, so there's a floor. MoEngage means I'm not starting from zero on data either. But I don't have product-layer intelligence yet, and that's the gap that worries me — right now I'm leaning on the regulatory moat holding, not on the product getting structurally harder to leave over time.
