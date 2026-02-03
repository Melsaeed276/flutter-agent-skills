# Skill: BLoC Overview (Events, States, Streams)

## Purpose
The BLoC pattern models user/system inputs as events and outputs as states. It is especially useful for event-driven domains and complex side effects.

## When to use
- You prefer event-driven modeling.
- You need strong separation between UI and business logic.
- Multiple UI widgets depend on the same event stream.

## When NOT to use
- For simple local state, a `StatefulWidget` may be enough.
- Do not create a BLoC for each tiny widget.

## Core concepts
- **Event**: input to the system.
- **State**: output snapshot.
- **Side effects**: navigation/toasts should be handled via listeners.

## Recommended patterns
- Keep events and states small and typed.
- Map exceptions to typed failures at boundaries.
- Use distinct handling for "refresh" vs "initial load".

## Minimal example

Conceptual structure (package-specific code omitted):

```text
UI -> add(Event)
BLoC -> emits(State)
UI listens -> renders + triggers side effects
```

## Edge cases
- Event storms (typing) need debounce.
- Concurrency: multiple events can interleave; define ordering rules.

## Common mistakes
- Putting navigation inside the BLoC.
- Emitting impossible state combinations.

## Testing strategy
- Test event -> state sequences with deterministic fakes.

## Related skills
- [Events and states](./events_states.md)
- [Side effects](./side_effects.md)
- [Testing BLoC](./testing.md)
