# Skill Index (Start Here)

This is the main router for the repository.

## Start here

- New to the codebase or stuck? Read [playbooks/debugging.md](./playbooks/debugging.md) and [quality_bar/definition_of_done.md](./quality_bar/definition_of_done.md).
- Building UI that must work everywhere? Start with [ui/responsive.md](./ui/responsive.md) → [ui/breakpoints.md](./ui/breakpoints.md) → [ui/adaptive_layouts.md](./ui/adaptive_layouts.md).
- Targeting foldables? Start with [ui/foldables.md](./ui/foldables.md) and also read [platform/foldables.md](./platform/foldables.md).

## Domains (map)

- Dart fundamentals: [dart/SKILL.md](./dart/SKILL.md)
- Flutter core mechanics: [flutter_core/SKILL.md](./flutter_core/SKILL.md)
- State management: [state/SKILL.md](./state/SKILL.md)
- Navigation: [navigation/SKILL.md](./navigation/SKILL.md)
- Architecture: [architecture/SKILL.md](./architecture/SKILL.md)
- Data (networking/storage/serialization): [data/SKILL.md](./data/SKILL.md)
- UI (Material/Cupertino/responsive/foldables): [ui/SKILL.md](./ui/SKILL.md)
- Platform integrations: [platform/SKILL.md](./platform/SKILL.md)
- Testing: [testing/SKILL.md](./testing/SKILL.md)
- Performance: [performance/SKILL.md](./performance/SKILL.md)
- Build & release: [build_release/SKILL.md](./build_release/SKILL.md)
- Advanced: [advanced/SKILL.md](./advanced/SKILL.md)

## Decision tree (what file should I open?)

Use the first match:

1. **“My UI breaks on tablets/desktop/web.”** → [ui/responsive.md](./ui/responsive.md) → [ui/breakpoints.md](./ui/breakpoints.md) → [flutter_core/layout_constraints.md](./flutter_core/layout_constraints.md)
2. **“Foldable / dual-screen behavior.”** → [ui/foldables.md](./ui/foldables.md) → [platform/foldables.md](./platform/foldables.md)
3. **“Unexpected rebuilds / jank.”** → [performance/rebuilds.md](./performance/rebuilds.md) → [performance/jank.md](./performance/jank.md) → [flutter_core/rendering_pipeline.md](./flutter_core/rendering_pipeline.md)
4. **“Async bugs, loading/error UX.”** → [dart/async.md](./dart/async.md) → [state/shared/async_state.md](./state/shared/async_state.md) → [architecture/error_modeling.md](./architecture/error_modeling.md)
5. **“Navigation & deep links.”** → [navigation/go_router/overview.md](./navigation/go_router/overview.md) → [navigation/go_router/deep_links.md](./navigation/go_router/deep_links.md)
6. **“Data layer is messy.”** → [architecture/repository_pattern.md](./architecture/repository_pattern.md) → [data/SKILL.md](./data/SKILL.md)
7. **“Tests are flaky/slow.”** → [testing/SKILL.md](./testing/SKILL.md) → [testing/ci_testing.md](./testing/ci_testing.md)
8. **“I need a safe refactor path.”** → [playbooks/refactoring.md](./playbooks/refactoring.md) → [quality_bar/code_review_checklist.md](./quality_bar/code_review_checklist.md)

## Explicit responsive + foldables entry points

- Responsive foundations: [ui/responsive.md](./ui/responsive.md)
- Breakpoint strategy: [ui/breakpoints.md](./ui/breakpoints.md)
- Adaptive layout patterns: [ui/adaptive_layouts.md](./ui/adaptive_layouts.md)
- Foldables UI patterns: [ui/foldables.md](./ui/foldables.md)
- Foldables platform considerations: [platform/foldables.md](./platform/foldables.md)

