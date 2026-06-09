# Kill Switch Audit

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** |Both NGX/Infoware (equities order routing) and NIBSS/NIP (wallet funding and NIP transfers) are single-source. There is no alternative provider for NGX order execution — it is a regulated monopoly. NIBSS has partial alternatives via direct bank APIs but none are configured. | H / M / L | Document every NGX and NIBSS API call and payload format now.|
| **Abstraction** | | H / M / L | |
| **Routing** | | H / M / L | |
| **Eval** | | H / M / L | |

## Portability Score
<!-- Ready / Partial / Locked -->

## If [primary vendor] doubles pricing tomorrow:
<!-- What's your 48-hour response? -->

## If [primary vendor] ships a competing product:
<!-- What's defensible that they can't replicate? -->
