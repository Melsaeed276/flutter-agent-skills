# Widget Lifecycle

## Mental model

- Widgets are immutable descriptions; elements hold the mutable connection to render objects.
- State lives in `State` objects and survives rebuilds when identity is stable.

## Patterns

- Subscribe in `initState`, update subscriptions in `didUpdateWidget`, cancel in `dispose`.
- Keep side effects out of `build`.

## Pitfalls

- Triggering network calls in `build` causes repeated requests.
- Late async results calling `setState` after dispose.

## Example (subscription lifecycle)

```dart
late final StreamSubscription<int> _sub;

@override
void initState() {
  super.initState();
  _sub = Stream<int>.periodic(const Duration(seconds: 1), (i) => i).listen((_) {});
}

@override
void dispose() {
  _sub.cancel();
  super.dispose();
}
```

