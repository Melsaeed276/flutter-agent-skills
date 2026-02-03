# Skill: Caching and Invalidation (State-Level)

## Purpose
Caching reduces latency and load, but it introduces complexity: staleness, invalidation, and consistency.
This doc provides patterns for modeling cache behavior in state so it stays explicit and testable.

## When to use
- You want instant UI with background refresh.
- You have paginated lists or offline-friendly screens.
- Multiple screens share the same data.

## When NOT to use
- Do not cache everything by default; caches are a liability.
- Do not hide caching in UI widgets; centralize it in data/state layers.

## Core concepts
- **Freshness**: when cached data is acceptable.
- **Invalidation**: what events make cache stale (logout, mutation, TTL).
- **Consistency**: optimistic vs server-authoritative.

## Recommended patterns
- Choose a strategy: cache-aside or stale-while-revalidate.
- Track timestamps and invalidation reasons.
- Invalidate on writes (mutations) and auth changes.
- Keep cache keying explicit (user ID, filters, locale).

## Minimal example

A tiny cache metadata wrapper:

```dart
class Cached<T> {
  final T value;
  final DateTime fetchedAt;

  const Cached({required this.value, required this.fetchedAt});

  bool isStale(Duration ttl, DateTime now) => now.difference(fetchedAt) > ttl;
}
```

## Edge cases
- Per-user caches: never leak data across users.
- Filtered lists: cache key must include filters/sort.
- Offline: decide if you show stale data with a banner.

## Common mistakes
- Using a global singleton cache without invalidation.
- Forgetting to invalidate after mutations.

## Testing strategy
- Unit test TTL expiration and invalidation triggers.
- Integration test: mutation updates list + details screens consistently.

## Related skills
- [Caching strategies (data layer)](../../data/local_storage/caching_strategies.md)
- [Repository pattern](../../architecture/repository_pattern.md)
- [Token refresh](../../data/networking/token_refresh.md)
