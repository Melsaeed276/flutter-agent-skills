# Skill: Safe Refactoring Playbook

## Purpose
This playbook helps you refactor Flutter/Dart code safely: preserve behavior, avoid regressions, and keep changes reviewable.

## When to use
- You want to introduce a new architecture boundary (repositories, DI, feature modules).
- You need to replace a state management approach or navigation structure.
- You are paying down tech debt in a high-churn area.

## When NOT to use
- Emergency hotfix with minimal scope; use a targeted patch (but still add a regression test).

## Core concepts
- **Behavior lock-in**: tests and snapshots of expected behavior before changing internals.
- **Strangler pattern**: migrate incrementally behind an interface.
- **Thin slices**: ship refactors in small, reviewable PRs.

## Recommended patterns
- Start with a feature boundary and define an interface (e.g., repository).
- Add tests around existing behavior *before* changing implementation.
- Migrate one call site at a time; keep old + new paths temporarily.
- Use feature flags only when necessary; remove them quickly.
- Add a rollback plan: what would you revert if issues appear.

## Minimal example

A safe refactor sequence:

```text
1) Identify boundary (e.g., "User profile fetch").
2) Add tests around existing behavior.
3) Introduce interface + adapter; keep current impl behind it.
4) Move call sites to the interface.
5) Replace impl (new data source / caching / error model).
6) Delete old impl; rerun tests; verify perf.
```

## Edge cases
- Large UI refactors: preserve keys and semantics to avoid losing state; see [flutter_core/keys.md](../flutter_core/keys.md).
- Async refactors: avoid changing timing; add tests that assert ordering and cancellation.
- Navigation changes: deep links and back stack behavior can regress silently.

## Common mistakes
- Refactoring without tests; reviewers cannot validate behavior.
- Mixing refactor and new features; increases risk and review time.
- Breaking public APIs used across packages.

## Testing strategy
- Add regression tests first.
- For refactors involving routing, add an integration test that covers:
  - deep link entry
  - back navigation
  - state restoration if applicable

## Related skills
- [Quality bar: Code review checklist](../quality_bar/code_review_checklist.md)
- [Architecture: Feature structure](../architecture/feature_structure.md)
- [Architecture: Repository pattern](../architecture/repository_pattern.md)
