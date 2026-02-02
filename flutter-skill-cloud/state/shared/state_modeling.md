# State Modeling

## Mental model

State is a snapshot of everything the UI needs to render *right now*.

## Patterns

- Prefer immutable state objects.
- Keep domain rules in use-cases/services, not in widgets.
- Model transitions explicitly (what causes state to change).

## Pitfalls

- “Boolean soup” (`isLoading`, `hasError`, `isEmpty`) that can become inconsistent.

## See also

- Async state: async_state.md
- Error modeling: ../../architecture/error_modeling.md

