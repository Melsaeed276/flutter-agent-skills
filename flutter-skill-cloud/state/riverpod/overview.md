# Skill: Riverpod Overview

## Purpose
Riverpod provides a structured way to manage state and dependencies with testable, composable providers.
This doc describes the mental model and when to use common provider types.

## When to use
- You need dependency injection and state management together.
- You want testable async flows (caching, retry, refresh).
- You want to avoid `BuildContext`-based DI.

## When NOT to use
- Do not use Riverpod for everything; keep UI-local state in widgets when simple.
- Do not expose providers that return DTOs directly to UI.

## Core concepts
- **Provider**: a function of dependencies -> value.
- **Ref**: reads/watches and manages lifecycles.
- **AutoDispose**: dispose when unused; careful with caching.

## Recommended patterns
- Keep providers feature-scoped.
- Put side effects in notifiers (commands), not in widgets.
- Use `ProviderContainer` for unit tests.

## Minimal example

A simple counter with `Notifier`:

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

final counterProvider = NotifierProvider<Counter, int>(Counter.new);

class Counter extends Notifier<int> {
  @override
  int build() => 0;

  void increment() => state = state + 1;
}
```

## Edge cases
- `autoDispose` can cause unexpected reloads when switching tabs.
- Providers can be recomputed if dependencies change.

## Common mistakes
- Doing async work directly in widgets.
- Using providers as global singletons without feature boundaries.

## Testing strategy
- Unit test notifiers with `ProviderContainer`.
- Widget test provider wiring with `ProviderScope`.

## Related skills
- [Providers](./providers.md)
- [Notifiers](./notifiers.md)
- [Testing Riverpod](./testing.md)
