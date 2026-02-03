# Skill: Dart Null Safety

## Purpose
Null safety is a design tool: it turns runtime crashes into compile-time feedback.
This doc focuses on using null safety to model real data and to reduce defensive code in Flutter apps.

## When to use
- You see null dereference crashes.
- API responses have optional/missing fields.
- You are designing public APIs (widgets, services, repositories).

## When NOT to use
- Do not use `late` or `!` to bypass modeling; fix the types.
- Do not make everything nullable "just in case"; it spreads checks everywhere.

## Core concepts
- **Non-nullable by default**: prefer `String` over `String?`.
- **Nullable types**: `T?` forces you to handle the absence case.
- **Promotion**: `if (x != null)` narrows `x` to non-null within the scope.
- **Sentinel values**: using empty strings/0 instead of null often hides bugs.

## Recommended patterns
- Model optional fields at the boundary (DTOs), then map to non-null domain types.
- Prefer `required` parameters for essential inputs.
- Use `??` / `??=` for safe defaults where appropriate.
- Avoid `late` unless initialization is guaranteed and documented.

## Minimal example

DTO (nullable) -> Domain (non-null) mapping:

```dart
class UserDto {
  final String? id;
  final String? displayName;

  const UserDto({required this.id, required this.displayName});

  factory UserDto.fromJson(Map<String, Object?> json) {
    return UserDto(
      id: json['id'] as String?,
      displayName: json['display_name'] as String?,
    );
  }
}

class User {
  final String id;
  final String displayName;

  const User({required this.id, required this.displayName});

  factory User.fromDto(UserDto dto) {
    return User(
      id: dto.id ?? 'unknown',
      displayName: (dto.displayName ?? '').trim().isEmpty
          ? 'Anonymous'
          : dto.displayName!.trim(),
    );
  }
}
```

## Edge cases
- Collections: `List<T?>` vs `List<T>?` mean very different things.
- `late` fields can throw at runtime if accessed too early.
- JSON `null` vs missing keys: handle both at parsing.

## Common mistakes
- Sprinkling `!` everywhere instead of mapping types once.
- Making widget parameters nullable when the widget cannot render without them.
- Using `dynamic` and losing the benefits of null safety.

## Testing strategy
- Unit test DTO parsing with missing/invalid keys.
- Add tests for defaulting behavior (e.g., anonymous name).

## Related skills
- [Serialization: JSON parsing](../data/serialization/json_parsing.md)
- [DTO vs entity](../architecture/dto_vs_entity.md)
- [Error modeling](../architecture/error_modeling.md)
