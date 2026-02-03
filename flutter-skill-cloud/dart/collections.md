# Skill: Dart Collections and Immutability

## Purpose
Most Flutter state bugs are data-shape bugs: lists mutate unexpectedly, maps are partially updated, or identity changes cause rebuild churn.
This doc shows patterns for safe collection updates and immutable state.

## When to use
- You manage state as lists/maps and updates are hard to reason about.
- You see UI not updating (mutations without notifying) or updating too much.
- You want safer APIs for models.

## When NOT to use
- Do not use deep copies everywhere; copy only what changes.
- Do not prematurely introduce heavy immutable libraries if simple patterns suffice.

## Core concepts
- **Structural sharing**: copy only the changed parts.
- **Unmodifiable views**: prevent accidental mutation.
- **Equality/identity**: immutable models make equality meaningful.

## Recommended patterns
- Store `List`/`Map` as `final` and expose unmodifiable copies.
- Update collections with copy-on-write: `[...]`, `{...}`.
- Prefer `const` where possible (compile-time immutability).
- Avoid mutating a list in place if it is part of UI/state.

## Minimal example

Immutable state with copy-on-write list updates:

```dart
class Todo {
  final String id;
  final String title;
  final bool done;

  const Todo({required this.id, required this.title, required this.done});

  Todo copyWith({String? title, bool? done}) {
    return Todo(
      id: id,
      title: title ?? this.title,
      done: done ?? this.done,
    );
  }
}

class TodosState {
  final List<Todo> todos;

  const TodosState({required this.todos});

  TodosState add(Todo todo) {
    return TodosState(todos: [...todos, todo]);
  }

  TodosState toggle(String id) {
    return TodosState(
      todos: [
        for (final t in todos)
          if (t.id == id) t.copyWith(done: !t.done) else t,
      ],
    );
  }
}
```

## Edge cases
- Sorting in place (`list.sort`) mutates; copy first: `final next = [...list]..sort(...)`.
- Maps with nested objects require nested copy-on-write.

## Common mistakes
- Mutating a list inside state and expecting listeners to rebuild.
- Returning internal mutable lists from models.

## Testing strategy
- Unit test collection transforms: add/toggle/remove.
- Assert old state remains unchanged (immutability guarantee).

## Related skills
- [State modeling](../state/shared/state_modeling.md)
- [Rebuild cost](../performance/rebuilds.md)
- [Error handling](./error_handling.md)
