# go_router Guards

## Mental model

Guards decide whether a location is allowed (auth, onboarding, feature flags).

## Patterns

- Make guard dependencies explicit (auth state provider, config).
- Avoid async guard loops; keep decisions quick and deterministic.

