# Skill: State Modeling (Immutable, Explicit, Small)

## Purpose
Good state models make UI predictable: they clearly represent what the user can see and do.
This doc focuses on modeling state explicitly (loading/data/error/empty), keeping it immutable, and separating UI state from domain state.

## When to use
- UI state is a pile of booleans (`isLoading`, `hasError`, `isEmpty`) that can contradict.
- You need clearer transitions and fewer conditional branches.
- You want easier testing.

## When NOT to use
- Do not create overly generic "mega" states for unrelated screens.
- Do not put transport concerns (DTOs, HTTP codes) into UI state.

## Core concepts
- **State is data**: a snapshot at time T.
- **Events/commands**: inputs that produce the next state.
- **Invariants**: rules your state must always satisfy.

## Recommended patterns
- Prefer one state object per screen/feature.
- Use sealed classes (or tagged enums) for mutually exclusive states.
- Keep state fields `final`; update with `copyWith`.

## Minimal example

A small explicit state model:

```dart
sealed class ProfileState {
  const ProfileState();
}

class ProfileLoading extends ProfileState {
  const ProfileLoading();
}

class ProfileLoaded extends ProfileState {
  final String name;
  const ProfileLoaded(this.name);
}

class ProfileError extends ProfileState {
  final String message;
  const ProfileError(this.message);
}
```

## Edge cases
- Empty vs loaded: decide if empty is a distinct state.
- Partial data: consider a state for "stale data + refreshing".

## Common mistakes
- Multiple booleans that allow impossible combinations.
- Making state mutable and updating fields in place.

## Testing strategy
- Unit test transitions: loading -> loaded, loading -> error.
- Widget test rendering for each state.

## Related skills
- [Async state](./async_state.md)
- [Caching state](./caching_state.md)
- [Error modeling](../../architecture/error_modeling.md)
