# Caching State

## Mental model

Caches exist to trade freshness for speed, reliability, and cost. Make that trade explicit.

## Patterns

- Cache at the repository boundary.
- Store metadata: `fetchedAt`, `staleAfter`, and source (`network` vs `cache`).
- Implement invalidation rules (time-based, manual, or event-based).

## Pitfalls

- Hidden caches that make debugging impossible.
- Stale UI because refresh and invalidation aren’t modeled.

## See also

- Caching strategies: ../../data/local_storage/caching_strategies.md

