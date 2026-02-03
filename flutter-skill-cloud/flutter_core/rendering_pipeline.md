# Skill: Flutter Rendering Pipeline (Build, Layout, Paint)

## Purpose
Understanding the rendering pipeline helps you debug performance and visual issues: why frames drop, why a repaint happens, and how to isolate work.

## When to use
- You see jank or dropped frames.
- Animations are stuttery.
- Repaints happen when you don't expect them.

## When NOT to use
- Do not micro-optimize without measuring; start with [performance/devtools.md](../performance/devtools.md).

## Core concepts
- **Build**: create widgets; should be fast.
- **Layout**: compute sizes/positions under constraints.
- **Paint**: draw; can be expensive for complex scenes.
- **Compositing**: GPU layers; `RepaintBoundary` can isolate repaints.

## Recommended patterns
- Keep `build` pure and cheap (no parsing, sorting, or I/O).
- Use `RepaintBoundary` around expensive painters that animate independently.
- Prefer implicit animations for simple transitions.
- Avoid unnecessary opacity layers and large shadows.

## Minimal example

Isolating repaints for a frequently-updating child:

```dart
import 'package:flutter/material.dart';

class RepaintExample extends StatelessWidget {
  final Widget ticking;
  final Widget heavy;

  const RepaintExample({super.key, required this.ticking, required this.heavy});

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        // Only this subtree repaints when ticking changes.
        const RepaintBoundary(child: _Clock()),
        // Heavy static UI should not repaint unnecessarily.
        RepaintBoundary(child: heavy),
      ],
    );
  }
}

class _Clock extends StatefulWidget {
  const _Clock();

  @override
  State<_Clock> createState() => _ClockState();
}

class _ClockState extends State<_Clock> {
  late final Ticker _ticker;
  int _ticks = 0;

  @override
  void initState() {
    super.initState();
    _ticker = Ticker((_) => setState(() => _ticks++))..start();
  }

  @override
  void dispose() {
    _ticker.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) => Text('$_ticks');
}
```

## Edge cases
- `RepaintBoundary` can increase memory usage; measure before and after.
- Some widgets repaint due to inherited changes (theme, media query).

## Common mistakes
- Wrapping everything in `RepaintBoundary` blindly.
- Putting expensive computation in `build`.

## Testing strategy
- Use DevTools frame charts and repaint rainbow to confirm improvements.
- Add widget tests to lock in visual behavior; use goldens for layout.

## Related skills
- [Performance: DevTools](../performance/devtools.md)
- [Performance: Rebuilds](../performance/rebuilds.md)
- [Animations](../ui/animations.md)
