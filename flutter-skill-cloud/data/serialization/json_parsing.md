# JSON Parsing

## Patterns

- Parse at the boundary; keep raw maps out of UI/state.
- Tolerant readers: ignore unknown fields and handle missing optional fields.

## Pitfalls

- Treating untrusted JSON as fully valid without validation.

