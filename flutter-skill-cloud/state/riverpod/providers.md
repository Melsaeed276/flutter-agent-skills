# Skill: Riverpod Providers (Types, Composition, Families)

## Purpose
Provider choice affects correctness (lifecycle, caching) and readability. This doc covers common provider types and when to use `family` and `autoDispose`.

## When to use
- You need to expose derived data or dependencies.
- You need parameterized providers (`family`) for IDs/filters.
- You need async data (`FutureProvider`, `StreamProvider`, `AsyncNotifier`).

## When NOT to use
- Do not create providers for ephemeral UI state (text field focus).
- Avoid deep provider graphs that are hard to reason about.

## Core concepts
- **Provider**: pure derived value.
- **(Async)NotifierProvider**: command + state.
- **Family**: parameterized provider.
- **autoDispose**: frees resources when unused.

## Recommended patterns
- Use `Provider` for pure computation.
- Use `Notifier/AsyncNotifier` for mutable state.
- Use `family` for entity IDs and filters.
- Add caching explicitly if you use `autoDispose`.

## Minimal example

Parameterized provider for a user id:

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

final userNameProvider = FutureProvider.family<String, String>((ref, userId) async {
  // Replace with repository call.
  await Future<void>.delayed(const Duration(milliseconds: 10));
  return 'User $userId';
});
```

## Edge cases
- `family` keys must be stable and comparable.
- Avoid `autoDispose` on providers that must keep cache across navigation.

## Common mistakes
- Using `FutureProvider` for mutable state updates (use `AsyncNotifier`).
- Rebuilding expensive providers on every key stroke.

## Testing strategy
- Unit test providers via `ProviderContainer` and overrides.

## Related skills
- [Async patterns](./async_patterns.md)
- [Architecture](./architecture.md)
- [Testing](./testing.md)
