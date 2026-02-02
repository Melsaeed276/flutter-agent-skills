# BLoC Side Effects

## Mental model

Side effects include navigation, toasts, analytics, and starting async work.

## Patterns

- Prefer one-direction flow: event → effect/state.
- Keep effects testable (inject interfaces).

## Pitfalls

- Triggering navigation inside build based on state without guarding.

