# Memory

## Patterns

- Avoid holding large decoded images in memory longer than needed.
- Dispose controllers and subscriptions.
- Prefer caching with eviction, not unbounded growth.

## Pitfalls

- Global singletons holding onto contexts/controllers.

