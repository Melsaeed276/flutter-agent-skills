# Skill: Dart Error Handling (Exceptions vs Typed Failures)

## Purpose
Flutter apps need predictable failures: user messages, retries, and analytics should be consistent.
This doc describes when to throw exceptions and when to model errors as data.

## When to use
- You need consistent error UX (retry, empty state, auth expired).
- You are defining repository/service boundaries.
- You want tests that assert specific failures.

## When NOT to use
- Do not model every unexpected programmer error as a typed failure; assertions/exceptions are fine for invariants.
- Do not throw exceptions for expected outcomes (e.g., "not found").

## Core concepts
- **Programmer errors**: invariant violations; crash early with asserts.
- **Expected failures**: network timeouts, validation errors; model as data.
- **Boundary mapping**: convert low-level errors to domain failures at the boundary.

## Recommended patterns
- Use a `Result<T>`/`Either`-style type for boundary returns.
- Centralize mapping from exceptions -> failures.
- Keep failure types small and user-meaningful.

## Minimal example

A tiny `Result<T>` type:

```dart
sealed class Result<T> {
  const Result();
}

class Ok<T> extends Result<T> {
  final T value;
  const Ok(this.value);
}

class Err<T> extends Result<T> {
  final Failure failure;
  const Err(this.failure);
}

sealed class Failure {
  const Failure();
}

class NetworkFailure extends Failure {
  final String message;
  const NetworkFailure(this.message);
}

Future<Result<String>> loadGreeting() async {
  try {
    // Replace with a real call.
    return const Ok('Hello');
  } catch (e) {
    return const Err(NetworkFailure('Please check your connection.'));
  }
}
```

## Edge cases
- Retries should not retry on all failures (e.g., 4xx validation errors).
- Some errors should trigger logout/reauth; treat them explicitly.

## Common mistakes
- Catching `Exception` broadly and losing stack traces/log context.
- Returning null to indicate failure (ambiguous).

## Testing strategy
- Unit test the mapping: given an exception type, you get the expected failure.
- Widget test the error UI: message + retry action.

## Related skills
- [Architecture: Error modeling](../architecture/error_modeling.md)
- [State: Async state](../state/shared/async_state.md)
- [Networking: Token refresh](../data/networking/token_refresh.md)
