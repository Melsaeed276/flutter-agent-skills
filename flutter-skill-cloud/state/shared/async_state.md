# Async State

## Mental model

Most async UI state is one of:

- `idle` (optional)
- `loading`
- `data`
- `empty` (optional, derived or explicit)
- `error`

## Patterns

- Store the last successful data if it improves UX during refresh.
- Distinguish “initial load” from “refresh” for better UI.

## Pitfalls

- Clearing data on refresh creates flicker.
- Showing transport-level errors directly to users.

## Example (sealed state)

```dart
sealed class AsyncState<T> {
  const AsyncState();
}
class Loading<T> extends AsyncState<T> { const Loading(); }
class Data<T> extends AsyncState<T> { final T value; const Data(this.value); }
class Failure<T> extends AsyncState<T> { final Object error; const Failure(this.error); }
```

## See also

- Dart async: ../../dart/async.md
- Testing state: testing_state.md

