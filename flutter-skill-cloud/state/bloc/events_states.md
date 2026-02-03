# Skill: BLoC Events and States (Modeling and Invariants)

## Purpose
Well-designed events and states are the heart of a maintainable BLoC. This doc shows how to model them to keep invariants explicit.

## When to use
- Your event/state classes are growing and hard to reason about.
- You have multiple loading modes (initial, refresh, pagination).

## When NOT to use
- Do not encode transport details (HTTP codes) into states; map them to failures.

## Core concepts
- **Mutually exclusive states**: model with sealed classes/unions.
- **Event intent**: events represent user/system intent, not implementation steps.

## Recommended patterns
- Use a distinct event for refresh vs load.
- Keep state immutable.
- Include enough data in state to render without extra lookups.

## Minimal example

Event and state shapes:

```dart
sealed class ProfileEvent {
  const ProfileEvent();
}

class LoadProfile extends ProfileEvent {
  const LoadProfile();
}

class RefreshProfile extends ProfileEvent {
  const RefreshProfile();
}

sealed class ProfileState {
  const ProfileState();
}

class ProfileLoading extends ProfileState {
  const ProfileLoading();
}

class ProfileLoaded extends ProfileState {
  final String name;
  final bool refreshing;
  const ProfileLoaded(this.name, {this.refreshing = false});
}

class ProfileFailure extends ProfileState {
  final Object error;
  const ProfileFailure(this.error);
}
```

## Edge cases
- Pagination adds a "loading more" sub-state.
- Errors during refresh should not always clear existing data.

## Common mistakes
- Using booleans that can conflict (`isLoading` and `hasData`).
- Emitting states that require extra async reads to render.

## Testing strategy
- Test state sequences for load and refresh separately.

## Related skills
- [Async state modeling](../shared/async_state.md)
- [Error modeling](../../architecture/error_modeling.md)
- [Testing BLoC](./testing.md)
