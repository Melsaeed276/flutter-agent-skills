# Testing State

## What to test

- State transitions: given inputs/events, state changes are correct.
- Error cases and retries.
- Caching/invalidation behavior.

## Patterns

- Use fake repositories with deterministic responses.
- Test time with a controllable clock abstraction.

## Pitfalls

- Over-mocking: prefer fakes over deep mocks for readability.

## See also

- Unit tests: ../../testing/unit_tests.md
- Mocking: ../../testing/mocking.md

