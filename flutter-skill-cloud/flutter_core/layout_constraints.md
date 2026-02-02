# Layout Constraints

## Mental model

Constraints flow down, sizes flow up, parents set positions.

- A child must pick a size within the constraints it receives.
- “Unbounded” typically means “infinite max” in one axis.

## Patterns

- Use `LayoutBuilder` when decisions depend on available space.
- Use `Flexible/Expanded` in `Row/Column` to avoid overflow.

## Pitfalls

- Putting a scrollable inside another scrollable without constraints.
- Using fixed sizes that work on phones but fail on tablets/desktop.

## Example (constraint-aware)

```dart
LayoutBuilder(
  builder: (context, constraints) {
    final isWide = constraints.maxWidth >= 600;
    return isWide ? const Text('Wide') : const Text('Narrow');
  },
);
```

## See also

- Responsive UI: ../ui/responsive.md
- Breakpoints: ../ui/breakpoints.md

