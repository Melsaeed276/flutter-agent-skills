# Skill: Definition of Done (Flutter)

## Purpose
This checklist defines what must be true before a change is considered "done" and safe to ship.

## When to use
- Before merging a PR.
- Before cutting a release.
- After fixing a bug to ensure it stays fixed.

## When NOT to use
- Never fully skip it. For hotfixes, explicitly mark which items are deferred.

## Core concepts
- **Evidence**: each item should have an observable signal (test, screenshot, log, metric).
- **Regression prevention**: bug fixes require tests.
- **Portability**: no environment-specific assumptions.

## Recommended patterns
- Treat this as a contract between author and reviewer.
- Prefer small PRs that can satisfy the checklist easily.

## Minimal example

```text
[ ] Repro steps documented (bugfix) or acceptance criteria listed (feature).
[ ] Appropriate tests added/updated (unit/widget/integration).
[ ] No new analyzer warnings; formatting applied.
[ ] UX states covered: loading, empty, error, retry.
[ ] Performance checked for the changed screen/flow.
[ ] Platform checks done if relevant (iOS/Android/web/desktop).
[ ] Release notes impact noted (if user-visible).
```

## Edge cases
- Large refactors: ensure behavior lock-in with tests and staged rollout.
- Foldables/responsive UIs: validate multiple sizes and posture changes.

## Common mistakes
- "Works on my phone" without tests or screenshots.
- Forgetting back navigation and deep links.

## Testing strategy
- Bugfix: add a regression test for the failing scenario.
- Feature: add at least one golden/widget test for critical layout and one integration test for the main flow.

## Related skills
- [Code review checklist](./code_review_checklist.md)
- [Performance checklist](./performance_checklist.md)
- [Architecture review checklist](./architecture_review_checklist.md)
