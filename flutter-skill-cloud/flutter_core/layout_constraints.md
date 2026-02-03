# Skill: Layout Constraints (Overflows, Unbounded, Sizing)

## Purpose
Most Flutter layout bugs are constraint bugs. Understanding constraints prevents trial-and-error widget stacking and makes responsive design easier.

## When to use
- Overflows (yellow/black stripes) occur.
- You see errors like "RenderFlex children have non-zero flex but incoming height constraints are unbounded".
- Widgets get unexpected sizes.

## When NOT to use
- Do not fix constraint issues with `IntrinsicHeight/Width` unless you must; they can be expensive.

## Core concepts
- **Constraints go down**: parent tells child max/min size.
- **Sizes go up**: child chooses a size within constraints.
- **Parent sets position**: layout determines placement.
- **Unbounded**: scroll views often provide unbounded constraints along the scroll axis.

## Recommended patterns
- Use `LayoutBuilder` to read constraints and choose layout.
- Use `Expanded/Flexible` only inside bounded flex parents.
- Wrap content in `ConstrainedBox` when you need explicit bounds.
- For scrollable columns, use slivers or `SizedBox` to bound flex children.

## Minimal example

Choosing layout based on width constraints:

```dart
import 'package:flutter/material.dart';

class ResponsivePanel extends StatelessWidget {
  const ResponsivePanel({super.key});

  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(
      builder: (context, constraints) {
        if (constraints.maxWidth >= 840) {
          return const Row(
            children: [
              Expanded(child: Placeholder()),
              VerticalDivider(width: 1),
              Expanded(child: Placeholder()),
            ],
          );
        }
        return const Placeholder();
      },
    );
  }
}
```

## Edge cases
- `Expanded` inside `SingleChildScrollView` (unbounded height) will throw.
- `ListView` inside `Column` needs a bounded height (use `Expanded`).

## Common mistakes
- Wrapping everything in `SingleChildScrollView` to "fix" overflow.
- Using `IntrinsicHeight` to fix flex issues instead of fixing constraints.

## Testing strategy
- Widget tests at multiple surface sizes (phone/tablet/desktop constraints).
- Golden tests for critical layouts.

## Related skills
- [UI: Responsive](../ui/responsive.md)
- [UI: Breakpoints](../ui/breakpoints.md)
- [BuildContext](./build_context.md)
