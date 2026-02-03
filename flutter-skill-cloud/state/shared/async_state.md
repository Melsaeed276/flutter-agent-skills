# Skill: Async State (Loading, Error, Data, Retry)

## Purpose
Async work drives most apps: loading screens, retries, pagination, and background refresh.
A consistent async state model prevents "infinite spinner" bugs and makes error UX predictable.

## When to use
- You load data from network/storage.
- You need retry and refresh behavior.
- You see races (stale data overwriting new).

## When NOT to use
- For one-off local computation, a simple `FutureBuilder` may be enough.
- Do not hide errors; represent them explicitly.

## Core concepts
- **Async phases**: idle/loading/success/failure.
- **Retry**: same command with same inputs.
- **Refresh**: fetch again and update while showing previous data.

## Recommended patterns
- Prefer explicit states over multiple booleans.
- Store last successful data when refreshing (stale-while-refresh).
- Use typed failures at boundaries; map to user messages at UI.

## Minimal example

An async state with refresh support:

```dart
sealed class AsyncState<T> {
  const AsyncState();
}

class AsyncLoading<T> extends AsyncState<T> {
  const AsyncLoading();
}

class AsyncData<T> extends AsyncState<T> {
  final T value;
  final bool isRefreshing;
  const AsyncData(this.value, {this.isRefreshing = false});
}

class AsyncError<T> extends AsyncState<T> {
  final Object error;
  const AsyncError(this.error);
}
```

## Edge cases
- Concurrent loads: decide whether to cancel, dedupe, or allow parallel.
- Errors with stale data: show the old data but surface a non-blocking error.

## Common mistakes
- Treating refresh as a full-screen loading state.
- Retrying without clearing stale request IDs (stale responses overwrite).

## Testing strategy
- Unit test: refresh keeps previous data while `isRefreshing=true`.
- Widget test: error state shows retry affordance.

## Related skills
- [Dart async](../../dart/async.md)
- [Caching state](./caching_state.md)
- [Riverpod async patterns](../riverpod/async_patterns.md)
