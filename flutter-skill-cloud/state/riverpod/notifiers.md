# Riverpod Notifiers

## Mental model

Notifiers own mutable state but expose immutable snapshots.

## Patterns

- Keep side effects in notifier methods or use-cases.
- Model async state explicitly ([../shared/async_state.md](../shared/async_state.md)).

## Pitfalls

- Re-entrancy: multiple overlapping requests updating state out of order.

