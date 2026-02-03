# Skill: Dart Async (Futures, Streams, Cancellation)

## Purpose
Async bugs are among the most expensive Flutter bugs: they are timing-dependent and often appear only on slow devices.
This doc provides a mental model for Futures/Streams and patterns to keep async work correct, cancellable, and testable.

## When to use
- You see "setState() called after dispose()" or actions running after navigation.
- Multiple requests race and UI shows stale data.
- You need retries, timeouts, debouncing, or cancellation.

## When NOT to use
- For CPU-heavy work, prefer isolates; see [isolates.md](./isolates.md).
- For UI-specific lifecycle rules, see [flutter_core/widget_lifecycle.md](../flutter_core/widget_lifecycle.md).

## Core concepts
- **Future**: one eventual value or error.
- **Stream**: many values over time; you must manage subscriptions.
- **Ownership**: which object is responsible for cancelling/ignoring async work.
- **Staleness**: newer requests should supersede older ones.

## Recommended patterns
- Tie async work to an owner and cancel/ignore on dispose.
- Use request "generation" counters to ignore stale responses.
- Always add timeouts for network calls; propagate typed failures.
- Prefer `async`/`await` for readability; avoid deeply nested `.then` chains.

## Minimal example

A widget-safe async pattern that ignores stale results:

```dart
import 'package:flutter/material.dart';

class SearchBox extends StatefulWidget {
  const SearchBox({super.key});

  @override
  State<SearchBox> createState() => _SearchBoxState();
}

class _SearchBoxState extends State<SearchBox> {
  int _requestId = 0;
  String _result = '';

  Future<String> _fakeSearch(String q) async {
    await Future<void>.delayed(const Duration(milliseconds: 300));
    return 'Result for "$q"';
  }

  Future<void> onQueryChanged(String q) async {
    final int requestId = ++_requestId;

    final String value;
    try {
      value = await _fakeSearch(q).timeout(const Duration(seconds: 2));
    } catch (e) {
      // Map to a typed failure in real code.
      return;
    }

    // Ignore stale responses.
    if (!mounted || requestId != _requestId) return;

    setState(() {
      _result = value;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        TextField(onChanged: onQueryChanged),
        Text(_result),
      ],
    );
  }
}
```

## Edge cases
- Streams can keep running if you forget to cancel the subscription.
- Errors in streams require `onError` handling or `try/catch` around `await for`.
- Retries can amplify load; use backoff and a max attempt count.

## Common mistakes
- Updating UI after an `await` without checking `mounted`.
- Sharing a single Future across changing inputs (stale cache).
- Swallowing errors (empty `catch`) and losing diagnostics.

## Testing strategy
- Unit test ordering: ensure stale responses do not overwrite newer ones.
- Use `fake_async` or controlled clocks where helpful.
- Prefer small tests that assert the state transition sequence.

## Related skills
- [State: Async state](../state/shared/async_state.md)
- [Flutter lifecycle](../flutter_core/widget_lifecycle.md)
- [Networking timeouts](../data/networking/dio.md)
