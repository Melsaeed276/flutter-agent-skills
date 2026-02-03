# Skill: Testing Riverpod (ProviderContainer, Overrides)

## Purpose
Riverpod is test-friendly when you structure dependencies as providers and use overrides.
This doc provides patterns for unit and widget tests.

## When to use
- You want to test notifiers/providers without widgets.
- You need to inject fakes in tests.

## When NOT to use
- Do not write widget tests to validate pure provider logic.

## Core concepts
- **ProviderContainer**: runs providers without Flutter.
- **Overrides**: replace providers with fakes.
- **Listeners**: observe state changes.

## Recommended patterns
- Use `ProviderContainer` for unit tests.
- Use overrides for repositories/clients.
- Keep notifiers small and deterministic.

## Minimal example

Unit test shape (pseudo):

```dart
// In a test file:
// final container = ProviderContainer(overrides: [repoProvider.overrideWithValue(FakeRepo())]);
// addTearDown(container.dispose);
// final notifier = container.read(controllerProvider.notifier);
// await notifier.load();
// expect(container.read(controllerProvider), isA<Loaded>());
```

## Edge cases
- AutoDispose providers may dispose in tests; keep them alive or read them appropriately.

## Common mistakes
- Over-mocking and asserting internal calls.
- Forgetting to dispose the container.

## Testing strategy
- Unit tests for provider logic.
- Widget tests for provider -> UI rendering.

## Related skills
- [Unit tests](../../testing/unit_tests.md)
- [Widget tests](../../testing/widget_tests.md)
- [Shared testing state](../shared/testing_state.md)
