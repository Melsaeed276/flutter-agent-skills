# Repository Pattern

## Mental model

Repositories isolate data retrieval details (network/cache/mapping) behind a stable interface.

## Patterns

- Repository returns domain models or typed failures.
- Keep mapping at boundaries (DTO → domain entity).

## Pitfalls

- Repository leaks transport concepts (HTTP status, JSON maps) into UI.

## See also

- Mappers: ../data/serialization/mappers.md
- Caching: ../state/shared/caching_state.md

