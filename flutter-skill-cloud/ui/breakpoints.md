# Breakpoints

## Goal

Provide a **consistent, app-wide strategy** for choosing layout variants across phones, tablets, desktop, and web.

## Recommended breakpoint tiers

Use width-based tiers (from `LayoutBuilder` constraints), with optional height cues for edge cases:

- **Compact**: `< 600` (most phones)
- **Medium**: `600–839` (large phones, small tablets portrait)
- **Expanded**: `840–1199` (tablets landscape, small desktop)
- **Large**: `>= 1200` (desktop/web)

## Pattern: central breakpoint helper

```dart
enum Breakpoint { compact, medium, expanded, large }

Breakpoint breakpointFor(double width) {
  if (width < 600) return Breakpoint.compact;
  if (width < 840) return Breakpoint.medium;
  if (width < 1200) return Breakpoint.expanded;
  return Breakpoint.large;
}
```

## Pitfalls

- Using `MediaQuery` width everywhere (fails in split panes and dialogs).
- Many arbitrary breakpoints per screen (inconsistent UX).

## Testing guidance

- Pick canonical test widths: `390`, `600`, `840`, `1200`.
- Verify typography and tap targets at larger text scales.

## See also

- Responsive vs adaptive: responsive.md
- Adaptive layouts: adaptive_layouts.md

