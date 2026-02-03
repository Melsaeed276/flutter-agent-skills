# Skill: Clean Architecture (Layers and Dependency Direction)

## Purpose
Clean architecture separates policy (business rules) from details (Flutter framework, HTTP clients, databases). It improves testability and makes it easier to change implementations.

## When to use
- You have complex business rules.
- You need to swap data sources (REST -> GraphQL, local cache).
- You want to unit test domain logic without Flutter.

## When NOT to use
- Do not add layers for simple CRUD screens; complexity should justify it.

## Core concepts
- **Domain**: entities, value objects, use-cases, repository interfaces.
- **Data**: API clients, DTOs, database; implements repositories.
- **Presentation**: widgets + state controllers.
- **Dependency rule**: outer layers depend on inner abstractions.

## Recommended patterns
- Keep domain free of Flutter imports.
- Map DTOs -> entities at the data boundary.
- Model failures in the domain layer.

## Minimal example

Layered flow:

```text
UI -> Controller -> UseCase -> Repository (interface) -> RepositoryImpl -> API/DB
```

## Edge cases
- Over-layering can slow development; apply only where boundaries pay off.
- Shared domain models across features can become a coupling point.

## Common mistakes
- Domain depending on data layer types.
- Throwing exceptions across layers without mapping.

## Testing strategy
- Unit test use-cases with fake repositories.
- Contract test repository implementations.

## Related skills
- [Repository pattern](./repository_pattern.md)
- [DTO vs entity](./dto_vs_entity.md)
- [Error modeling](./error_modeling.md)
