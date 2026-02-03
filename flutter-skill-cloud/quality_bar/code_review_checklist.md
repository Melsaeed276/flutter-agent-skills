# Skill: Code Review Checklist (Flutter/Dart)

## Purpose
A reviewer-focused checklist to catch correctness, API design, maintainability, and test gaps.

## When to use
- Reviewing a PR.
- Self-review before requesting review.

## When NOT to use
- Do not use it as a blocking bureaucracy for trivial changes; scale the depth with risk.

## Core concepts
- **Risk-based review**: focus on correctness and regressions first.
- **Boundaries**: keep UI/state/domain/data separations clear.
- **Tests as evidence**: prefer tests over comments.

## Recommended patterns
- Validate correctness on edge cases (nulls, empty lists, slow network, offline).
- Check API ergonomics: names, types, nullability, error contracts.
- Look for lifecycle hazards: async after dispose, context misuse.
- Ensure state is observable and deterministic.

## Minimal example

```text
[ ] Does the change have a clear purpose and minimal diff?
[ ] Are loading/error/empty states handled?
[ ] Is error modeling consistent (typed failures, actionable messages)?
[ ] Any async lifecycle risks (mounted checks, cancellation)?
[ ] Tests added/updated; do they fail before the fix?
[ ] No unnecessary rebuilds or heavy work on the UI thread.
```

## Edge cases
- Navigation changes: check deep links, back stack, and nested routes.
- Data layer changes: check pagination, caching, token refresh race conditions.

## Common mistakes
- Over-mocking in tests (tests become coupled to implementation).
- Putting business logic in widgets.

## Testing strategy
- Ask for the smallest test that proves the behavior:
  - unit for pure logic
  - widget for UI wiring
  - integration for multi-screen flows

## Related skills
- [Definition of done](./definition_of_done.md)
- [Architecture review checklist](./architecture_review_checklist.md)
- [Testing hub](../testing/SKILL.md)
