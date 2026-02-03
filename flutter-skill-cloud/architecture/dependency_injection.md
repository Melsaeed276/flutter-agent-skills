# Skill: Dependency Injection (Constructors, Providers, Service Locators)

## Purpose
Dependency injection makes code testable and replaceable by avoiding hard-coded global singletons.
This doc focuses on pragmatic DI in Flutter: constructor injection first, then containers when needed.

## When to use
- You need to replace a real API client with a fake in tests.
- You need environment configuration (staging/prod) or white-label.
- You want to avoid `BuildContext`-based global lookups.

## When NOT to use
- Do not introduce a DI framework for a tiny project if constructors are enough.
- Avoid hidden global registries with mutable state.

## Core concepts
- **Constructor injection**: explicit dependencies.
- **Composition root**: where you wire implementations.
- **Override**: replace dependencies for tests.

## Recommended patterns
- Prefer constructor parameters for leaf objects.
- Centralize wiring in one module (app root).
- Keep dependency graphs shallow.

## Minimal example

Constructor injection with a composition root:

```dart
abstract class Clock {
  DateTime now();
}

class SystemClock implements Clock {
  @override
  DateTime now() => DateTime.now();
}

class GreetingService {
  final Clock clock;
  const GreetingService(this.clock);

  String greeting() => clock.now().hour < 12 ? 'Morning' : 'Hello';
}

GreetingService buildGreetingService() {
  return GreetingService(SystemClock());
}
```

## Edge cases
- Singletons: acceptable for pure, stateless services but avoid mutable global state.
- Async initialization: keep it explicit and testable.

## Common mistakes
- Hiding dependencies behind `static` accessors.
- Passing `BuildContext` into services.

## Testing strategy
- Unit test with fake dependencies.

## Related skills
- [Riverpod architecture](../state/riverpod/architecture.md)
- [Feature structure](./feature_structure.md)
- [White label](../advanced/white_label.md)
