# Error Modeling

## Goal

Provide consistent, user-friendly failures that are testable and do not leak transport details.

## Patterns

- Define an app-wide failure type (or small set of failure categories).
- Include:
  - stable code (for analytics/support)
  - user message (localized)
  - diagnostic context (log-only)

## Pitfalls

- Exposing raw exceptions to UI.
- Mixing “empty result” with “error” without clarity.

## See also

- Dart error handling: ../dart/error_handling.md
- Async state: ../state/shared/async_state.md

