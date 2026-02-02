# Adaptive Layouts

## Goal

Switch **structure**, not just spacing, based on device class or available space.

## Pattern: navigation rail vs bottom navigation

- **Compact**: bottom navigation (thumb reach, limited width)
- **Expanded/Large**: navigation rail or drawer (more space, better discoverability)

## Pattern: master-detail

- **Compact**: separate routes (list → detail)
- **Expanded/Large**: two-pane (list + detail simultaneously)

## Pattern: split view shell

Use a “shell” that owns navigation chrome; keep feature screens focused on content.

## Pitfalls

- Resetting detail selection on resize (bad continuity).
- Different information architecture across sizes (confusing mental model).

## Testing guidance

- Verify resizing continuity: selection, scroll position, and form edits persist.
- Add widget tests for “two-pane vs one-pane” routing decisions.

## See also

- Breakpoints: breakpoints.md
- Foldables: foldables.md
- Navigation: ../navigation/SKILL.md

