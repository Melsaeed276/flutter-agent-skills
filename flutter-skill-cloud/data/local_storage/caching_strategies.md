# Caching Strategies

## Mental model

Caching is policy: decide what to cache, for how long, and how to invalidate.

## Patterns

- Time-based TTL for “mostly static” data.
- Manual invalidation after writes.
- Stale-while-revalidate for better UX.

## Pitfalls

- Cache without invalidation becomes data corruption with a nice UI.

## See also

- Caching state: ../../state/shared/caching_state.md

