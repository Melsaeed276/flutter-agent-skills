# Skill: Error Modeling (Typed Failures and UX)

## Purpose
Users need actionable errors and consistent retry behavior. Typed failures make it possible to implement consistent UX and analytics.

## When to use
- You have network + cache + auth errors.
- Different screens handle errors inconsistently.
- You want better test coverage of error paths.

## When NOT to use
- Do not create dozens of failure types; keep a small taxonomy.
- Do not leak low-level exceptions to UI.

## Core concepts
- **Failure taxonomy**: network, unauthorized, validation, not found, unknown.
- **Boundary mapping**: translate exceptions/HTTP codes to failures.
- **User messaging**: map failures to localized messages.

## Recommended patterns
- Define failures in the domain layer.
- Map at the data boundary.
- Keep user messages separate from technical diagnostics.

## Minimal example

A small failure set:

```dart
sealed class Failure {
  const Failure();
}

class Unauthorized extends Failure {
  const Unauthorized();
}

class NetworkDown extends Failure {
  const NetworkDown();
}

class UnknownFailure extends Failure {
  final Object error;
  const UnknownFailure(this.error);
}
```

## Edge cases
- Token refresh loops: treat as a distinct failure and stop retrying.
- Partial success: some pages may render partial data with inline errors.

## Common mistakes
- Using strings as error types.
- Retrying on validation errors.

## Testing strategy
- Unit test mapping rules (exception -> failure).
- Widget test error UI and retry actions.

## Related skills
- [Dart error handling](../dart/error_handling.md)
- [Token refresh](../data/networking/token_refresh.md)
- [Async state](../state/shared/async_state.md)
