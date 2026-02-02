# Debugging Playbook

## Goal

Find the smallest explanation that matches the symptoms, then add a regression test.

## Triage checklist

- Reproduce deterministically (record exact steps, inputs, device class).
- Reduce scope (first failing screen, first failing state transition).
- Check for lifecycle issues (background/foreground, navigation pops, hot reload artifacts).
- Verify assumptions about constraints (see [flutter_core/layout_constraints.md](../flutter_core/layout_constraints.md)).

## Common Flutter failure modes

- “It rebuilds too much” → check `const`, `keys`, and state placement ([performance/rebuilds.md](../performance/rebuilds.md)).
- “Layout overflows only on some devices” → breakpoint mismatch or unconstrained child ([ui/breakpoints.md](../ui/breakpoints.md)).
- “Async completes after dispose” → cancel/ignore late results ([dart/async.md](../dart/async.md)).

## Debug loop

1. Add logging at boundaries (API → repository → state → UI).
2. Make the state explicit (loading/success/empty/error).
3. Write one focused test that captures the bug.
4. Fix, then refactor toward the intended architecture.

