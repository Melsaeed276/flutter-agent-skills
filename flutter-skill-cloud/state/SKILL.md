# State Skills

## What this domain covers

How to model and manage state in Flutter apps: shared principles, async state, caching, testing, plus patterns for Riverpod and BLoC.

## When to read it

- Your UI has inconsistent loading/error behavior.
- Business rules leak into widgets.
- Multiple features need shared caching or invalidation.

## Subtopics

- Shared fundamentals:
  - [shared/state_modeling.md](./shared/state_modeling.md)
  - [shared/async_state.md](./shared/async_state.md)
  - [shared/caching_state.md](./shared/caching_state.md)
  - [shared/testing_state.md](./shared/testing_state.md)
- Riverpod:
  - [riverpod/overview.md](./riverpod/overview.md)
  - [riverpod/providers.md](./riverpod/providers.md)
  - [riverpod/notifiers.md](./riverpod/notifiers.md)
  - [riverpod/async_patterns.md](./riverpod/async_patterns.md)
  - [riverpod/architecture.md](./riverpod/architecture.md)
  - [riverpod/testing.md](./riverpod/testing.md)
- BLoC:
  - [bloc/overview.md](./bloc/overview.md)
  - [bloc/events_states.md](./bloc/events_states.md)
  - [bloc/side_effects.md](./bloc/side_effects.md)
  - [bloc/testing.md](./bloc/testing.md)

## Decision guide

- If you need **a consistent loading/error model**, go to [shared/async_state.md](./shared/async_state.md).
- If you need **caching and invalidation**, go to [shared/caching_state.md](./shared/caching_state.md).
- If you need **provider primitives and composition**, go to [riverpod/providers.md](./riverpod/providers.md).
- If you need **event-driven flows**, go to [bloc/events_states.md](./bloc/events_states.md).

