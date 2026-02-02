# Null Safety

## Mental model

- Prefer making invalid states unrepresentable by types.
- Use nullable types for “absent” only when absence is meaningful.

## Patterns

- Use required named parameters for invariants.
- Prefer `late final` only when initialization is guaranteed before access.
- Convert external data (JSON) to non-null domain models as early as possible.

## Pitfalls

- `!` is a promise you might not keep; treat it as a code smell.
- “nullable everywhere” pushes checks to the UI and increases bugs.

## Example

```dart
class User {
  final String id;
  final String displayName;
  const User({required this.id, required this.displayName});
}
```

## See also

- Data mappers: ../data/serialization/mappers.md

