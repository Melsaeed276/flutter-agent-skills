# Skill: Nested Routes (Tabs, ShellRoute, Two-Level Nav)

## Purpose
Nested navigation is required for tabs, drawers, or master-detail on large screens. It is also a common source of back-stack bugs.
This doc describes patterns that keep nested routing predictable.

## When to use
- You have bottom tabs with independent navigation stacks.
- You need a shell layout (nav rail + content).
- You need master-detail that keeps both panes.

## When NOT to use
- Do not create multiple navigators without a clear UX requirement.

## Core concepts
- **Shell**: shared scaffold around child routes.
- **Branch stacks**: each tab can have its own stack.
- **Back behavior**: must feel native on each platform.

## Recommended patterns
- Use a shell route for shared UI.
- Keep per-branch state isolated.
- Define a canonical "home" route for each branch.

## Minimal example

Conceptual shell structure:

```text
Shell (NavigationRail/Bar)
  - Branch A stack
  - Branch B stack
```

## Edge cases
- Deep links into a nested route must select the correct branch.
- Back button on Android should pop within the branch before exiting.

## Common mistakes
- Sharing the same navigator key across branches.
- Losing scroll position when switching tabs due to disposal.

## Testing strategy
- Integration test: deep link into nested route and verify branch selection.
- Widget test: back button pops within branch.

## Related skills
- [Adaptive layouts](../../ui/adaptive_layouts.md)
- [go_router testing](./testing.md)
- [Navigator pitfalls](../navigator_1/pitfalls.md)
