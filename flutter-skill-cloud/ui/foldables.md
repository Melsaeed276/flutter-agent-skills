# Foldables UI

## Concepts: hinge, posture, and continuity

- **Hinge/fold**: a physical separation that can occlude content.
- **Posture**: how the device is folded (flat, book-like, tabletop, tent).
- **Continuity**: preserving user progress when folding/unfolding or resizing.

Treat foldables as “dynamic large screens” with extra constraints (occlusion and posture).

## Two-pane layouts

### When to use two panes

- Content benefits from simultaneous context (list + detail, editor + preview).
- Navigation would otherwise be deep and repetitive on large screens.

### Content distribution patterns

- Left: navigation/list, Right: detail/content.
- Primary actions remain reachable in both panes.
- Avoid placing critical content under a hinge; keep safe margins.

## Continuity patterns (fold/unfold)

- Keep selection state stable (don’t reset to “first item”).
- Preserve scroll positions per pane (store `ScrollController` state carefully).
- Avoid rebuilding the entire app shell on posture change; limit scope.

## Navigation on foldables

- Prefer adaptive shell: bottom nav on compact; rail/drawer on expanded.
- For two-pane: deep links and back behavior must be deliberate.

## Practical widget approach

- Use `LayoutBuilder` for available width and apply [breakpoints.md](./breakpoints.md).
- Treat “occlusion” as padding/safe area when your platform integration provides it.
- Keep foldable-specific branching localized to layout components.

## Testing guidance (emulators)

- Validate behavior across:
  - narrow phone-like width
  - expanded “book/tablet-like” width
  - posture changes (flat ↔ folded) while editing/scrolling
- Add scenarios that verify continuity (selection + scroll + form state).

## See also

- Responsive fundamentals: responsive.md
- Adaptive layouts: adaptive_layouts.md
- Platform posture notes: ../platform/foldables.md

