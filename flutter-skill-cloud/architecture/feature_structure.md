# Feature Structure

## Goal

Make features easy to find, test, and modify without cross-feature coupling.

## Pattern (typical)

- `feature/`:
  - `ui/` widgets and screens
  - `state/` controllers/notifiers/blocs
  - `domain/` use-cases, policies
  - `data/` repositories, mappers, local/remote sources

## Pitfalls

- “shared” folder that becomes a dumping ground.
- Circular imports between features.

