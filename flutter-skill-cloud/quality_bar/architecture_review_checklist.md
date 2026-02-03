# Skill: Architecture Review Checklist

## Purpose
A checklist to keep architecture coherent across features: boundaries, dependencies, and evolution over time.

## When to use
- Introducing new layers (repositories, DI, caching).
- Adding cross-cutting concerns (analytics, auth, offline support).
- Splitting a monolith into packages/modules.

## When NOT to use
- Do not over-architect small prototypes. Start simple, then apply boundaries as complexity grows.

## Core concepts
- **Dependency direction**: UI -> domain -> data (or similar), never the reverse.
- **Replaceability**: boundaries exist so implementations can change.
- **Error contracts**: failures modeled consistently across layers.

## Recommended patterns
- Define interfaces at boundaries (repositories, clients).
- Keep DTOs out of UI; map to domain entities.
- Keep feature code grouped by feature, not by technical type only.
- Use DI to avoid global singletons.

## Minimal example

```text
[ ] Feature boundary is clear (folder/module).
[ ] Domain layer has no Flutter imports.
[ ] Data layer implements domain interfaces.
[ ] Errors are typed and mapped at the boundary.
[ ] Async flows have cancellation/timeout strategy.
[ ] Tests exist per layer.
```

## Edge cases
- Multi-brand/white-label: check that theme/config injection is not hard-coded.
- Platform-specific features: ensure platform code is isolated behind an interface.

## Common mistakes
- Leaking DTOs or API response shapes into UI/state.
- Circular dependencies between features.

## Testing strategy
- Unit tests for domain/use-cases.
- Contract tests for repositories (fake server or canned JSON).

## Related skills
- [Clean architecture](../architecture/clean_architecture.md)
- [Repository pattern](../architecture/repository_pattern.md)
- [Dependency injection](../architecture/dependency_injection.md)
