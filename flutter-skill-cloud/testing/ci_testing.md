# CI Testing

## Goal

Fast, deterministic tests that catch regressions early.

## Patterns

- Split fast unit/widget tests from slower integration tests.
- Quarantine flaky tests with a clear plan to fix.

## Pitfalls

- “Retry in CI” as a substitute for fixing nondeterminism.

