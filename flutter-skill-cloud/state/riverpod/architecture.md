# Skill: Riverpod Architecture (Boundaries and Organization)

## Purpose
Without structure, providers become a global soup. This doc describes how to organize providers by feature and layer, and how to keep boundaries clean.

## When to use
- The provider graph is hard to navigate.
- Features share repositories and need overrideable dependencies.
- You want consistent patterns across teams.

## When NOT to use
- Avoid creating a giant "core providers" file. Keep feature-local.

## Core concepts
- **Feature-first**: group providers with the feature.
- **Layering**: UI providers depend on domain/data providers, not the reverse.
- **Overrides**: testing and multi-brand configs.

## Recommended patterns
- Define repositories in the data layer; expose them as providers.
- Provide use-cases as providers when it improves composition.
- Keep "public" providers small; hide internal helpers.

## Minimal example

Feature structure suggestion:

```text
features/profile/
  data/profile_api_client.dart
  data/profile_repository_impl.dart
  domain/profile_repository.dart
  state/profile_controller.dart   (Notifier)
  ui/profile_screen.dart
```

## Edge cases
- Shared caches across features: define ownership and invalidation rules.
- Multi-account: ensure per-user scoping (provider keys include user id).

## Common mistakes
- Providers that return widgets or depend on `BuildContext`.
- Data layer depending on UI providers.

## Testing strategy
- Use provider overrides to inject fakes.
- Add contract tests for repositories.

## Related skills
- [Feature structure](../../architecture/feature_structure.md)
- [Repository pattern](../../architecture/repository_pattern.md)
- [Dependency injection](../../architecture/dependency_injection.md)
