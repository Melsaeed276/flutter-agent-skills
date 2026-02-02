# Pagination

## Mental model

Pagination is a state machine: initial load → next page → end reached → refresh.

## Patterns

- Keep “cursor/page token” as part of state.
- Prevent concurrent “load more” calls.

## Pitfalls

- Duplicates when items are appended without stable IDs.

## See also

- Keys: ../../flutter_core/keys.md
- Async state: ../../state/shared/async_state.md

