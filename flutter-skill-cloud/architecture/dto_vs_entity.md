# DTO vs Entity

## Mental model

- DTOs match transport/storage shapes (JSON, SQLite rows).
- Entities (domain models) match app concepts and invariants.

## Patterns

- Keep DTOs in data layer; convert to entities early.
- Entities should be easy to use in UI/state without null checks everywhere.

## Pitfalls

- Reusing DTOs in UI causes brittle coupling to backend changes.

