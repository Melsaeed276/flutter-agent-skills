# Skill: Feature Structure (Feature-First Organization)

## Purpose
A consistent folder structure reduces cognitive load and makes ownership clear. Feature-first organization scales better than purely technical layering (all widgets in one folder).

## When to use
- Features are inconsistent and hard to navigate.
- You want to modularize or extract packages.
- Multiple teams work in the same codebase.

## When NOT to use
- Do not split into packages too early; start with folders and clear boundaries.

## Core concepts
- **Feature-first**: group UI/state/domain/data per feature.
- **Shared core**: cross-cutting utilities live in a small `core/`.
- **Public API**: each feature exposes a limited surface.

## Recommended patterns
- Prefer `features/<name>/` with clear subfolders.
- Keep feature UI private unless reused.
- Avoid deep nesting; keep paths short.

## Minimal example

Suggested structure:

```text
lib/
  core/
    routing/
    theme/
    errors/
  features/
    auth/
      data/
      domain/
      state/
      ui/
    profile/
      ...
```

## Edge cases
- Cross-feature shared UI: extract a small `shared_ui/` or a package.
- Platform code: isolate it behind an interface.

## Common mistakes
- Creating a huge `utils/` folder (junk drawer).
- Sharing state across features via globals.

## Testing strategy
- Mirror structure in tests: `test/features/profile/...`.

## Related skills
- [Clean architecture](./clean_architecture.md)
- [Dependency injection](./dependency_injection.md)
- [Repository pattern](./repository_pattern.md)
