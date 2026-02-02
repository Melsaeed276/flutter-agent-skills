# Error Handling in Dart

## Mental model

- Exceptions are for truly exceptional control flow; domain failures are often better as typed results.
- Favor a single error model across layers.

## Patterns

- Convert low-level exceptions into an app-level failure type near the boundary.
- Include a stable code and a user-facing message separately.

## Pitfalls

- Catch-all `catch (e)` that loses stack traces or context.
- UI coupling to transport errors (HTTP codes) instead of domain failures.

## Example (typed failure)

```dart
sealed class Failure {
  const Failure();
}

class NetworkFailure extends Failure {
  final String message;
  const NetworkFailure(this.message);
}
```

## See also

- Error modeling: ../architecture/error_modeling.md
- Token refresh: ../data/networking/token_refresh.md

