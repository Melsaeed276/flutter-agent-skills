# DevTools

## What to look for

- Frame chart spikes (build/layout/paint).
- Widget rebuild counts and hot spots.
- Memory allocations and leaks.

## Pattern

1. Reproduce a jank moment.
2. Capture a trace.
3. Identify whether build, layout, or paint dominates.
4. Fix the dominating cost first.

