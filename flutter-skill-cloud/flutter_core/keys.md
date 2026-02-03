# Skill: Keys (Identity, State Preservation, Lists)

## Purpose
Keys tell Flutter how to match widgets to existing elements across rebuilds. Correct key usage prevents state loss, animation glitches, and list item mixups.

## When to use
- List items reorder/insert/remove and state should follow the item.
- You see wrong data in list tiles after updates.
- Forms/animations lose state unexpectedly.

## When NOT to use
- Do not add keys everywhere; keys have cost.
- Avoid widespread `GlobalKey`; use it only when you need cross-tree access.

## Core concepts
- **No key**: Flutter matches by position (index).
- **ValueKey**: matches by stable value (ID).
- **UniqueKey**: forces a new identity each build.
- **GlobalKey**: unique across the whole app; enables state lookup.

## Recommended patterns
- Use `ValueKey` for list items keyed by a stable ID.
- Prefer keys on the list item root, not on inner widgets.
- Use `GlobalKey` sparingly (forms, scaffold) and keep it stable.

## Minimal example

List reordering with stable keys:

```dart
import 'package:flutter/material.dart';

class Todo {
  final String id;
  final String title;
  const Todo(this.id, this.title);
}

class TodoList extends StatelessWidget {
  final List<Todo> todos;
  const TodoList({super.key, required this.todos});

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: todos.length,
      itemBuilder: (context, index) {
        final t = todos[index];
        return ListTile(
          key: ValueKey(t.id),
          title: Text(t.title),
        );
      },
    );
  }
}
```

## Edge cases
- Keys must be unique among siblings; duplicates cause subtle bugs.
- Using `UniqueKey` breaks state preservation (intentionally).

## Common mistakes
- Using `ValueKey(index)`; it changes when you reorder.
- Creating a new `GlobalKey()` in `build`.

## Testing strategy
- Widget test reorder: pump list, reorder items, verify state follows ID.

## Related skills
- [Rebuilds](../performance/rebuilds.md)
- [Widget lifecycle](./widget_lifecycle.md)
- [Animations](../ui/animations.md)
