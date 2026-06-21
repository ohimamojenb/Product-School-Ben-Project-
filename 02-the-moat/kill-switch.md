# Kill Switch Audit

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** |Both NGX/Infoware (equities order routing) and NIBSS/NIP (wallet funding and NIP transfers) are largely single-source at the provider level. There is no alternative provider for NGX order execution, it is a regulated monopoly, though we do have a direct NGX integration as a routing fallback (see Routing below). NIBSS has partial alternatives via direct bank APIs but none are configured.| H | Document every NGX and NIBSS API call and payload format now.
| **Abstraction** | There is no abstraction layer between our platform and either NGX/Infoware or NIBSS. Integration logic is built directly against their specific APIs and payload formats, meaning any change on their side requires direct code changes on ours, and switching providers would mean a full rebuild rather than a swap.| H |Map every point in the codebase where NGX/Infoware or NIBSS calls are made directly, so the blast radius of a forced switch is known. |
| **Routing** |Equities order flow primarily routes through Infoware to NGX, but we also have a direct integration with NGX itself, meaning Infoware downtime doesn't fully strand equities execution, we can fail over to the direct NGX connection. Wallet funding and transfers, however, still route exclusively through NIBSS/NIP, with no secondary rail configured for failover on that side. | M |Document and stress-test the direct NGX failover path to confirm it's production-ready, and identify the trigger for switching from Infoware to direct NGX. Separately, begin scoping bank-direct API alternatives for NIBSS/NIP, since that side still has zero redundancy. |
| **Eval** |We have no automated way to evaluate or detect when NGX/Infoware or NIBSS responses are degraded, delayed, or returning errors at scale, issues are typically caught reactively, through customer complaints or manual monitoring, not through systematic checks. |M|Stand up basic uptime/latency monitoring on both integrations so degradation is caught before customers report it. |

## Portability Score
<!-- Ready / Partial / Locked -->

## If [primary vendor] doubles pricing tomorrow:
<!-- What's your 48-hour response? -->

## If [primary vendor] ships a competing product:
<!-- What's defensible that they can't replicate? -->
