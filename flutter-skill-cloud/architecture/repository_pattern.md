# Skill: Repository Pattern (Boundary Between Domain and Data)

## Purpose
Repositories hide data source details (HTTP, DB, caching) behind a stable interface. This keeps UI and domain logic independent from transport/storage.

## When to use
- You need caching, offline support, or multiple data sources.
- You want to unit test without real network/DB.
- You want to change APIs without rewriting UI/state.

## When NOT to use
- Do not create repositories that are thin pass-throughs with no boundary value.

## Core concepts
- **Repository interface**: lives in domain.
- **Implementation**: lives in data.
- **Mapping**: DTO <-> entity at the boundary.

## Recommended patterns
- Return typed results (entities + failures).
- Keep repository methods aligned to use-cases (not raw REST endpoints).
- Document caching/invalidation behavior.

## Minimal example

Interface + implementation shape:

```dart
abstract class ProfileRepository {
  Future<String> fetchDisplayName(String userId);
}

class ProfileRepositoryImpl implements ProfileRepository {
  @override
  Future<String> fetchDisplayName(String userId) async {
    // call API/DB here
    return 'User $userId';
  }
}
```

## Edge cases
- Pagination: repository should provide a stable pagination contract.
- Auth: token refresh should be handled below the repository boundary.

## Common mistakes
- Exposing DTOs to UI.
- Allowing repository methods to return null for error.

## Testing strategy
- Unit test repository interface via a fake.
- Contract test the real implementation with canned responses.

## Related skills
- [DTO vs entity](./dto_vs_entity.md)
- [Networking](../data/networking/dio.md)
- [Caching strategies](../data/local_storage/caching_strategies.md)
