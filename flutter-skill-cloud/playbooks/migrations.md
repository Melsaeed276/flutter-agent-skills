# Skill: Migration Playbook (Packages, APIs, Platforms)

## Purpose
This playbook provides a safe workflow for migrating dependencies, Flutter versions, routing/state libraries, or platform targets.

## When to use
- Upgrading Flutter/Dart SDK.
- Migrating navigation (Navigator 1.0 -> `go_router`).
- Migrating state management (legacy -> Riverpod/BLoC).
- Changing platform requirements (target SDK, iOS deployment target, desktop/web support).

## When NOT to use
- Small patch updates with no API changes; follow normal PR checks.

## Core concepts
- **Compatibility matrix**: SDK version, package versions, platform constraints.
- **Incremental migration**: keep app shippable at each step.
- **Golden signals**: tests, crash-free sessions, performance baselines.

## Recommended patterns
- Pin versions during the migration; unpin after stability.
- Upgrade in layers: tooling -> core packages -> app features.
- Keep migration PRs small; one subsystem at a time.
- Add "canary" integration tests for the most important flows.

## Minimal example

Migration checklist:

```text
1) Define scope and success criteria.
2) Create baseline: tests passing + performance smoke test.
3) Upgrade/migrate one layer.
4) Fix compilation + run unit/widget tests.
5) Run integration tests for critical flows.
6) Verify platform-specific behavior.
7) Update docs and remove deprecated code.
```

## Edge cases
- Web/desktop: routing, file access, and platform channels differ; see [advanced/web_desktop.md](../advanced/web_desktop.md).
- Release signing: migration can break CI/release config; see [build_release/signing.md](../build_release/signing.md).
- Token refresh/auth: subtle behavior changes can cause loops; see [data/networking/token_refresh.md](../data/networking/token_refresh.md).

## Common mistakes
- Upgrading many packages at once; hard to isolate breakages.
- Skipping integration tests; routing and platform changes often break only end-to-end.

## Testing strategy
- Unit tests for libraries.
- Widget tests for screens.
- Integration tests for flows: login, deep link, purchase, and push notification open.

## Related skills
- [Navigation: go_router setup](../navigation/go_router/setup.md)
- [State: Riverpod architecture](../state/riverpod/architecture.md)
- [Testing: CI testing](../testing/ci_testing.md)
