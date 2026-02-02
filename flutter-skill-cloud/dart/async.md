# Dart Async

## Mental model

- `Future` is a single result later; `Stream` is many results over time.
- Cancellation is cooperative (you often cancel subscriptions/tokens, not “kill” a `Future`).
- UI bugs often come from “late results” after a widget is disposed.

## Patterns

- Prefer `async/await` for readability; keep scopes small.
- For streams, manage subscription lifecycle (subscribe in init, cancel in dispose).
- Capture a request “epoch” to ignore stale results.

## Pitfalls

- Unhandled errors in `Future`s disappear until they crash later.
- Multiple concurrent requests overwrite each other without coordination.

## Example (ignore stale results)

```dart
class SearchController {
  int _epoch = 0;

  Future<List<String>> search(String query) async {
    final int myEpoch = ++_epoch;
    final results = await Future.delayed(const Duration(milliseconds: 200), () => [query]);
    if (myEpoch != _epoch) return const []; // stale
    return results;
  }
}
```

## See also

- Async state modeling: ../state/shared/async_state.md
- Widget lifecycle: ../flutter_core/widget_lifecycle.md

