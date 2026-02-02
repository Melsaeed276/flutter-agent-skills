# FFI

## Mental model

FFI crosses a trust and safety boundary: memory management and threading rules change.

## Patterns

- Keep FFI calls behind a small Dart API.
- Validate inputs and handle failures deterministically.

## Pitfalls

- Blocking the UI isolate with FFI calls.

