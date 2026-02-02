# Responsive UI

## Responsive vs adaptive (definitions)

- **Responsive UI**: the *same* screen reflows (sizes/spacing/columns) to fit available space.
- **Adaptive UI**: the screen *changes structure* (navigation rail vs bottom nav, master-detail) based on device class or constraints.

Most apps need both: responsive inside a layout, adaptive at app-shell/navigation level.

## Core tools

### MediaQuery

- Use for device-level information (screen size, text scale factor, padding/insets).
- Prefer `MediaQuery.sizeOf(context)` and `MediaQuery.paddingOf(context)` to avoid extra rebuilds when only one field is needed.

### LayoutBuilder

- Use when decisions depend on **parent constraints** (the most common source of responsive bugs).
- Prefer `constraints.maxWidth` over `MediaQuery` when a widget is inside a sidebar, dialog, or split view.

### OrientationBuilder

- Use when orientation meaningfully changes layout *and* you can keep continuity (don’t reset user progress).

## Common constraint pitfalls (and fixes)

- **Overflow in Row/Column**: child demands more than max constraint → use `Expanded/Flexible`, wrap text with `Flexible`, or redesign layout.
- **Unbounded height in Column**: scrollable inside Column without constraints → wrap scrollable in `Expanded` or give it a bounded height.
- **Using screen width for inner widgets**: breaks in split view → use `LayoutBuilder` at the widget boundary.

## Pattern: responsive scaffold layout

```dart
class ResponsiveScaffold extends StatelessWidget {
  final Widget narrowBody;
  final Widget wideBody;

  const ResponsiveScaffold({required this.narrowBody, required this.wideBody, super.key});

  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(
      builder: (context, c) {
        final isWide = c.maxWidth >= 840;
        return isWide ? wideBody : narrowBody;
      },
    );
  }
}
```

## Testing guidance

- Test at multiple sizes, not just “a phone”.
- Include at least one wide breakpoint and one “awkward” size (for example, small tablet portrait).
- Add golden tests for key responsive layouts when UI stability matters ([../testing/golden_tests.md](../testing/golden_tests.md)).

## See also

- Breakpoints: [breakpoints.md](./breakpoints.md)
- Adaptive layouts: [adaptive_layouts.md](./adaptive_layouts.md)
- Layout constraints: ../flutter_core/layout_constraints.md
- Foldables: [foldables.md](./foldables.md)

