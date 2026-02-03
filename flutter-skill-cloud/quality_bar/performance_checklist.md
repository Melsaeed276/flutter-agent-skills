# Skill: Performance Checklist (Flutter)

## Purpose
A checklist to prevent common performance regressions: jank, excessive rebuilds, memory churn, and large images.

## When to use
- Before release.
- When touching list/grid screens, animations, or image-heavy flows.
- When you see frame drops or high memory usage.

## When NOT to use
- Do not over-optimize early. Use it when a screen is user-critical or already slow.

## Core concepts
- **Frame budget**: UI thread work must fit into a frame.
- **Rebuild cost**: rebuilds are normal; *unnecessary* rebuilds are expensive.
- **Memory pressure**: large images and caches can crash low-end devices.

## Recommended patterns
- Profile first; optimize the proven bottleneck.
- Avoid heavy work in `build` (parsing, sorting, JSON decoding).
- Use `const` widgets and stable keys where helpful.
- Optimize images: sizes, caching, decode.

## Minimal example

```text
[ ] Profile in profile mode for the target device class.
[ ] No expensive work in build/layout.
[ ] Lists use lazy builders; items are cheap to build.
[ ] Images are sized/decoded appropriately.
[ ] No memory leaks (controllers, subscriptions disposed).
```

## Edge cases
- Release mode can behave differently; verify a perf-sensitive screen in release.
- Foldables and tablets can show more content; list item complexity matters.

## Common mistakes
- Blindly adding `RepaintBoundary` without measuring.
- Using `GlobalKey` widely (can increase work).

## Testing strategy
- Add performance smoke tests where feasible.
- Add golden tests for layout stability across sizes.

## Related skills
- [Jank](../performance/jank.md)
- [Rebuilds](../performance/rebuilds.md)
- [Images](../performance/images.md)
