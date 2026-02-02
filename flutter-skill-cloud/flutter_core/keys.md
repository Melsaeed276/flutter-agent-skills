# Keys

## Mental model

Keys control how Flutter matches old elements to new widgets across rebuilds.

## Patterns

- Use `ValueKey(id)` for list items with stable identity.
- Use `GlobalKey` sparingly (forms, scaffold, navigator) due to cost and coupling.

## Pitfalls

- Using list index as key causes state to “move” when items are inserted/removed.

## Example

```dart
ListView(
  children: users.map((u) => ListTile(key: ValueKey(u.id), title: Text(u.name))).toList(),
);
```

