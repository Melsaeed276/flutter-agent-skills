# Jank

## Mental model

Jank happens when a frame misses its budget due to expensive build/layout/paint or blocking work on the UI thread.

## Patterns

- Reduce work per frame (simplify widget tree, reduce rebuild scope).
- Move CPU work off-thread (isolates).
- Avoid heavy paint effects across large areas.

## Pitfalls

- Fixing symptoms (adding delays) instead of removing the cost.

## See also

- Rendering pipeline: ../flutter_core/rendering_pipeline.md
- DevTools: devtools.md

