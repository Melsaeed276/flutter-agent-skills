# Skill: Testing BLoC (Event -> State Sequences)

## Purpose
BLoC tests are most valuable when they verify behavior sequences: given events and fake dependencies, you see expected state emissions.

## When to use
- Bugs keep returning and you need regression tests.
- Your BLoC has non-trivial async flows (retry/refresh/pagination).

## When NOT to use
- Do not over-specify implementation (exact timing, internal calls) unless required.

## Core concepts
- **Given/When/Then**: scenario-driven tests.
- **Fake dependencies**: deterministic repositories.
- **Sequences**: order of emitted states.

## Recommended patterns
- Prefer fakes to mocks for repositories.
- Test error paths explicitly.
- Test cancellation/ignore-stale behavior when relevant.

## Minimal example

Test outline:

```text
Given: FakeRepo returns success
When: Add Load event
Then: emits [Loading, Loaded]

Given: FakeRepo throws
When: Add Load event
Then: emits [Loading, Failure]
```

## Edge cases
- Debounce/throttle: tests need control over time.
- Pagination: test load-more emits incremental states.

## Common mistakes
- One giant test with many asserts.
- Asserting internal calls instead of observable states.

## Testing strategy
- Unit tests for BLoC sequences.
- Widget tests for BLoC wiring and listeners.

## Related skills
- [Unit tests](../../testing/unit_tests.md)
- [Mocking](../../testing/mocking.md)
- [Shared testing state](../shared/testing_state.md)
