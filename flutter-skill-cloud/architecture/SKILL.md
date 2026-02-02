# Architecture Skills

## What this domain covers

How to structure features, manage dependencies, model errors, and keep boundaries clean between UI, domain, and data.

## When to read it

- The codebase is inconsistent across features.
- Data, state, and UI are tightly coupled.
- You need to introduce dependency injection or a repository layer.

## Subtopics

- Feature structure: [feature_structure.md](./feature_structure.md)
- Clean architecture: [clean_architecture.md](./clean_architecture.md)
- Dependency injection: [dependency_injection.md](./dependency_injection.md)
- Repository pattern: [repository_pattern.md](./repository_pattern.md)
- DTO vs entity: [dto_vs_entity.md](./dto_vs_entity.md)
- Error modeling: [error_modeling.md](./error_modeling.md)

## Decision guide

- If you need **folder and module consistency**, go to [feature_structure.md](./feature_structure.md).
- If you need **clear boundaries and dependency direction**, go to [clean_architecture.md](./clean_architecture.md).
- If you need **consistent failures across layers**, go to [error_modeling.md](./error_modeling.md).

