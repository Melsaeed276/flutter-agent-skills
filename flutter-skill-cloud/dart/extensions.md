# Extensions

## Mental model

Extensions add methods without inheritance. Use them to improve readability and reduce utility classes.

## Patterns

- Keep extensions small and domain-specific.
- Prefer explicit naming to avoid method conflicts.

## Pitfalls

- Too many broad extensions make code discovery harder.

## Example

```dart
extension StringX on String {
  bool get isBlank => trim().isEmpty;
}
```

