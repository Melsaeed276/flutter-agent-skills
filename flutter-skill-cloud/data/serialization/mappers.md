# Mappers (DTO ↔ Domain)

## Mental model

Mapping is where you enforce invariants: convert nullable/optional transport shapes into safe domain objects.

## Patterns

- `Dto.fromJson` stays permissive; mapper to domain enforces required fields.
- Keep mapping logic testable with small pure functions.

## Pitfalls

- UI depending on DTO types.

## Example (mapper)

```dart
class UserDto {
  final String? id;
  final String? name;
  UserDto({this.id, this.name});
}

class User {
  final String id;
  final String name;
  const User({required this.id, required this.name});
}

User toDomain(UserDto dto) {
  if (dto.id == null || dto.name == null) throw StateError('Invalid user DTO');
  return User(id: dto.id!, name: dto.name!);
}
```

