# Skill Index (Start Here)

## Purpose

This is the router for the repository. Use it to pick the smallest doc that answers your question.

## When to use

- You are not sure which domain owns your problem.
- You want a decision tree from symptom -> doc.

## When NOT to use

- If you already know the exact topic file, open it directly.

## Core concepts

- **Symptoms over solutions**: start from what you see (jank, overflow, auth loop) and route.
- **Hubs then leaf**: open the domain hub `SKILL.md` and then the leaf doc.

## Decision tree

Use the first match:

1) **"My UI breaks on tablets/desktop/web."**
   - [ui/responsive.md](./ui/responsive.md) -> [ui/breakpoints.md](./ui/breakpoints.md) -> [ui/adaptive_layouts.md](./ui/adaptive_layouts.md)

2) **"Foldable / dual-screen behavior."**
   - [ui/foldables.md](./ui/foldables.md) -> [platform/foldables.md](./platform/foldables.md)

3) **"Overflow / unbounded constraints / weird sizes."**
   - [flutter_core/layout_constraints.md](./flutter_core/layout_constraints.md) -> [flutter_core/build_context.md](./flutter_core/build_context.md)

4) **"Unexpected rebuilds / jank / dropped frames."**
   - [performance/jank.md](./performance/jank.md) -> [performance/devtools.md](./performance/devtools.md) -> [performance/rebuilds.md](./performance/rebuilds.md)

5) **"Async bugs / loading-error UX is inconsistent."**
   - [dart/async.md](./dart/async.md) -> [state/shared/async_state.md](./state/shared/async_state.md) -> [architecture/error_modeling.md](./architecture/error_modeling.md)

6) **"Navigation / deep links / web URLs."**
   - [navigation/go_router/overview.md](./navigation/go_router/overview.md) -> [navigation/go_router/deep_links.md](./navigation/go_router/deep_links.md)

7) **"Data layer is messy (DTOs, caching, token refresh)."**
   - [architecture/repository_pattern.md](./architecture/repository_pattern.md) -> [data/SKILL.md](./data/SKILL.md)

8) **"Tests are flaky/slow."**
   - [testing/ci_testing.md](./testing/ci_testing.md) -> [testing/widget_tests.md](./testing/widget_tests.md)

9) **"I need a safe refactor path."**
   - [playbooks/refactoring.md](./playbooks/refactoring.md) -> [quality_bar/code_review_checklist.md](./quality_bar/code_review_checklist.md)

## Domains (map)

- Dart fundamentals: [dart/SKILL.md](./dart/SKILL.md)
- Flutter core mechanics: [flutter_core/SKILL.md](./flutter_core/SKILL.md)
- State management: [state/SKILL.md](./state/SKILL.md)
- Navigation: [navigation/SKILL.md](./navigation/SKILL.md)
- Architecture: [architecture/SKILL.md](./architecture/SKILL.md)
- Data (networking/storage/serialization): [data/SKILL.md](./data/SKILL.md)
- UI (responsive/material/cupertino/foldables): [ui/SKILL.md](./ui/SKILL.md)
- Platform integrations: [platform/SKILL.md](./platform/SKILL.md)
- Testing: [testing/SKILL.md](./testing/SKILL.md)
- Performance: [performance/SKILL.md](./performance/SKILL.md)
- Build & release: [build_release/SKILL.md](./build_release/SKILL.md)
- Advanced: [advanced/SKILL.md](./advanced/SKILL.md)

## Common mistakes

- Opening too many docs at once; start small.
- Treating symptoms (UI) when the root cause is state/data/lifecycle.

## Edge cases

- Some bugs only reproduce on slow devices or in release mode; see [performance/jank.md](./performance/jank.md) and [build_release/SKILL.md](./build_release/SKILL.md).

## Testing strategy

- Add a regression test as soon as you identify the smallest reproducer.

## Related skills

- Global conventions: [META.md](./META.md)
- Templates: [templates/SKILL_TEMPLATE.md](./templates/SKILL_TEMPLATE.md)
