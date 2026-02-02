# Rendering Pipeline

## Mental model

Flutter work roughly flows through:

1. Build (widgets → elements)
2. Layout (constraints → sizes)
3. Paint (draw commands)
4. Compositing (layers) and rasterization (GPU)

## Why it matters

- Layout is where “unbounded constraints” and overflows happen.
- Paint is where overdraw and expensive effects show up.

## Patterns

- Avoid triggering layout in tight loops (don’t measure during build repeatedly).
- Prefer `RepaintBoundary` around complex animated subtrees.

## See also

- Jank: ../performance/jank.md
- Layout constraints: layout_constraints.md

