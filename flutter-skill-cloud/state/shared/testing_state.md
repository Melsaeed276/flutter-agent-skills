# Skill: Testing State (Deterministic Transitions)

## Purpose
State tests should be deterministic and describe behavior, not implementation.
This doc provides a strategy for testing state transitions, async flows, and side effects.

## When to use
- You are adding state management to a feature.
- Bugs keep returning; you need regression tests.
- Async flows are complex (retry, refresh, pagination).

## When NOT to use
- Do not over-mock; tests become brittle.
- Do not test widgets to validate pure business logic; unit test it.

## Core concepts
- **Arrange/Act/Assert**: define inputs and expected states.
- **Fakes over mocks**: for repositories/clients.
- **Controlled time**: make async deterministic.

## Recommended patterns
- Test the state sequence (loading -> data -> error).
- Use a fake repository with scripted responses.
- Separate "effects" from state (navigation, toasts).

## Minimal example

A simple fake repository for deterministic tests:

```dart
class FakeProfileRepo {
  String? name;
  Object? error;

  Future<String> fetchName() async {
    if (error != null) throw error!;
    return name ?? 'Anonymous';
  }
}
```

## Edge cases
- Concurrency: ensure stale results do not overwrite new ones.
- Retries: ensure retry uses the same inputs and resets error state.

## Common mistakes
- Asserting internal private fields instead of public outputs.
- Writing one giant test that covers too many cases.

## Testing strategy
- Unit test state/controller objects.
- Widget test the rendering of each state.

## Related skills
- [Unit tests](../../testing/unit_tests.md)
- [Widget tests](../../testing/widget_tests.md)
- [BLoC testing](../bloc/testing.md)
