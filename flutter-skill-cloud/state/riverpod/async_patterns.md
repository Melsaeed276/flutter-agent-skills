# Skill: Riverpod Async Patterns (Refresh, Dedupe, Cancellation)

## Purpose
Async patterns determine UX and correctness: deduping requests, refreshing, canceling, and handling auth refresh.
This doc provides patterns that keep async predictable and testable.

## When to use
- Multiple widgets trigger the same load.
- You need pull-to-refresh without losing data.
- You need cancellation/ignore-stale to avoid races.

## When NOT to use
- Do not add complexity if a single `FutureProvider` is enough.

## Core concepts
- **Dedupe**: avoid duplicate requests.
- **Ignore stale**: track request generation IDs.
- **Refresh**: keep old data while fetching new.

## Recommended patterns
- Keep async flows inside notifiers.
- Store a request id and ignore stale completions.
- Use `ref.keepAlive()` only with an explicit caching plan.

## Minimal example

Ignoring stale async work inside a notifier:

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

final searchProvider = NotifierProvider<SearchNotifier, String>(SearchNotifier.new);

class SearchNotifier extends Notifier<String> {
  int _req = 0;

  @override
  String build() => '';

  Future<void> search(String query) async {
    final int req = ++_req;
    final String result = await Future<String>.delayed(
      const Duration(milliseconds: 50),
      () => 'Result for $query',
    );

    if (req != _req) return; // stale
    state = result;
  }
}
```

## Edge cases
- AutoDispose: switching tabs may dispose and restart loads.
- Auth refresh: a 401 may trigger a refresh; guard against refresh loops.

## Common mistakes
- Starting a load from widget `build` without gating.
- Treating refresh as a full-screen loading state.

## Testing strategy
- Unit test: make two `search` calls; ensure only latest updates state.

## Related skills
- [Token refresh](../../data/networking/token_refresh.md)
- [Async state modeling](../shared/async_state.md)
- [Testing Riverpod](./testing.md)
