# Skill: Theming Foundations (ThemeData, Inherited, Extensions)

## Purpose
A coherent theme reduces duplication and makes apps easier to maintain (especially for multi-brand and dark/light modes).
This doc covers ThemeData basics, tokenization via `ThemeExtension`, and safe usage patterns.

## When to use
- You are adopting Material 3 or creating a design system.
- You see hard-coded colors/sizes across widgets.
- You need brand or runtime theme switching.

## When NOT to use
- Do not encode business logic into theme.
- Avoid using theme as a global service locator.

## Core concepts
- **ThemeData**: global visual defaults.
- **ColorScheme**: semantic colors (primary, surface, error).
- **Inherited widgets**: theme lookup uses `BuildContext`.
- **ThemeExtension**: custom tokens without global constants.

## Recommended patterns
- Use `ColorScheme` + `TextTheme`; avoid raw hex values.
- Create a small set of spacing/radius tokens.
- Prefer per-component styles derived from tokens.
- Keep theme changes centralized in one place.

## Minimal example

A tiny ThemeExtension for spacing:

```dart
import 'package:flutter/material.dart';

@immutable
class Spacing extends ThemeExtension<Spacing> {
  final double s;
  final double m;
  final double l;

  const Spacing({required this.s, required this.m, required this.l});

  @override
  Spacing copyWith({double? s, double? m, double? l}) {
    return Spacing(s: s ?? this.s, m: m ?? this.m, l: l ?? this.l);
  }

  @override
  Spacing lerp(ThemeExtension<Spacing>? other, double t) {
    if (other is! Spacing) return this;
    return Spacing(
      s: lerpDouble(s, other.s, t)!,
      m: lerpDouble(m, other.m, t)!,
      l: lerpDouble(l, other.l, t)!,
    );
  }
}

Spacing spacingOf(BuildContext context) =>
    Theme.of(context).extension<Spacing>()!;
```

## Edge cases
- Theme lookups cause rebuilds when theme changes; keep derived values small.
- Animating between themes requires `lerp` implementations.

## Common mistakes
- Hard-coding colors inside widgets.
- Defining too many tokens without semantic meaning.

## Testing strategy
- Golden tests for light/dark themes and key components.
- Widget tests for runtime theme switching.

## Related skills
- [UI: Theming tokens](../ui/theming_tokens.md)
- [UI: Material 3](../ui/material3.md)
- [Advanced: White label](../advanced/white_label.md)
