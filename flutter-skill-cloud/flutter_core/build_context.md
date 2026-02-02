# BuildContext

## Mental model

- `BuildContext` is a handle to a location in the widget tree.
- Many lookups (theme, localization, providers) search *up* the tree from that location.

## Patterns

- Use the closest context that has the dependencies you need.
- Avoid using `context` after `await` unless you check `mounted`.

## Pitfalls

- Calling `Navigator.of(context)` with a context below a nested navigator.
- Reading inherited widgets during `initState` when not allowed.

## Example (mounted check)

```dart
class MyState extends State<MyWidget> {
  Future<void> load() async {
    await Future<void>.delayed(const Duration(milliseconds: 100));
    if (!mounted) return;
    ScaffoldMessenger.of(context).showSnackBar(const SnackBar(content: Text('Done')));
  }
}
```

## See also

- Lifecycle: widget_lifecycle.md
- Navigation pitfalls: ../navigation/navigator_1/pitfalls.md

