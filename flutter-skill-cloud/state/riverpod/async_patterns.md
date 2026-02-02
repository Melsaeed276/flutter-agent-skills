# Riverpod Async Patterns

## Patterns

- Separate “load” and “refresh” to avoid flicker.
- Keep the latest successful data while refreshing.

## Pitfalls

- Triggering loads from `build` without guarding (causes loops).

## See also

- Dart async: ../../dart/async.md
- Widget lifecycle: ../../flutter_core/widget_lifecycle.md

