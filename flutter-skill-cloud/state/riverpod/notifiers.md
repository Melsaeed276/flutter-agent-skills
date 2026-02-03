# Skill: Riverpod Notifiers (Commands + State)

## Purpose
Notifiers encapsulate mutable state and commands. They keep widgets thin and make side effects testable.

## When to use
- You need to update state in response to user actions.
- You need to coordinate async work (load, refresh, save).

## When NOT to use
- Do not put UI concerns (snackbars, navigation) directly in the notifier; emit effects.
- Do not expose internal mutable objects.

## Core concepts
- **build()**: initial state and dependency reads.
- **state**: current immutable state.
- **ref**: access dependencies and lifecycle hooks.

## Recommended patterns
- Define small command methods: `load`, `refresh`, `toggle`.
- Keep each notifier responsible for one screen/feature.
- Use typed state and failures.

## Minimal example

A notifier that loads and refreshes:

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

sealed class LoadState {
  const LoadState();
}

class Loading extends LoadState {
  const Loading();
}

class Loaded extends LoadState {
  final String value;
  final bool refreshing;
  const Loaded(this.value, {this.refreshing = false});
}

class Failed extends LoadState {
  final Object error;
  const Failed(this.error);
}

final demoProvider = NotifierProvider<DemoNotifier, LoadState>(DemoNotifier.new);

class DemoNotifier extends Notifier<LoadState> {
  @override
  LoadState build() {
    return const Loading();
  }

  Future<void> load() async {
    state = const Loading();
    try {
      await Future<void>.delayed(const Duration(milliseconds: 10));
      state = const Loaded('ok');
    } catch (e) {
      state = Failed(e);
    }
  }
}
```

## Edge cases
- Concurrent calls: ensure `load` calls do not race.
- Dispose: use `ref.onDispose` for cleanup.

## Common mistakes
- Triggering loads from `build` repeatedly.
- Updating state from stale async completions.

## Testing strategy
- Unit test: call `load`, assert state sequence.

## Related skills
- [Shared async state](../shared/async_state.md)
- [Async patterns](./async_patterns.md)
- [Testing Riverpod](./testing.md)
