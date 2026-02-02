# Collections & Immutability

## Mental model

- Prefer immutable state: replace collections rather than mutating in place.
- In Flutter, immutability often reduces rebuild bugs and makes tests simpler.

## Patterns

- Treat lists/maps as values in state objects.
- Use `copyWith` on state to replace changed fields.

## Pitfalls

- Mutating a list in-place can break equality and cache invalidation.

## Example

```dart
class CartState {
  final List<String> items;
  const CartState(this.items);

  CartState add(String item) => CartState([...items, item]);
}
```

## See also

- State modeling: ../state/shared/state_modeling.md

