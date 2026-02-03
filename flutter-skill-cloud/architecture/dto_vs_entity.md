# Skill: DTO vs Entity (Keep Boundaries Clean)

## Purpose
DTOs represent external data shapes (JSON, DB rows). Entities represent domain concepts.
Mixing them couples UI and business logic to API details and makes refactors hard.

## When to use
- You integrate an API or database.
- You see UI code depending on JSON field names.
- You want stable domain logic despite API changes.

## When NOT to use
- Do not over-model; simple apps can map minimally.

## Core concepts
- **DTO**: often nullable, optional, versioned.
- **Entity**: business meaning, invariants, typically non-null.
- **Mapper**: boundary conversion.

## Recommended patterns
- Parse into DTOs at the boundary.
- Map once: DTO -> entity.
- Keep entities stable and validated.

## Minimal example

DTO to entity mapping:

```dart
class UserDto {
  final String? id;
  final String? email;
  const UserDto({required this.id, required this.email});
}

class User {
  final String id;
  final String email;
  const User({required this.id, required this.email});
}

User toEntity(UserDto dto) {
  return User(
    id: dto.id ?? 'unknown',
    email: dto.email ?? '',
  );
}
```

## Edge cases
- Backward compatibility: old APIs may omit fields.
- Localization/time zones: normalize at the boundary.

## Common mistakes
- Passing DTOs to widgets.
- Letting entities have optional fields everywhere.

## Testing strategy
- Unit test mapping with missing/invalid inputs.

## Related skills
- [JSON parsing](../data/serialization/json_parsing.md)
- [Mappers](../data/serialization/mappers.md)
- [Null safety](../dart/null_safety.md)
