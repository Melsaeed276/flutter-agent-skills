# Foldables (Platform Considerations)

## Device posture considerations

- Posture changes can happen while the app is running; treat them like resizing events with potential occlusion.
- Some platforms expose posture/hinge metrics; others do not (design to degrade gracefully).

## Practical guidance

- Keep a single source of truth for “available content area” (width/height + any occlusion padding).
- Prefer constraint-driven UI ([../ui/responsive.md](../ui/responsive.md)) and only add posture-specific branching where it’s unavoidable.

## Limitations and expectations

- Do not assume all foldables expose hinge geometry or posture events.
- Test behavior even when hinge info is unavailable (fallback to regular breakpoints).

## Links

- Foldables UI patterns: [../ui/foldables.md](../ui/foldables.md)
- Adaptive layouts: [../ui/adaptive_layouts.md](../ui/adaptive_layouts.md)

