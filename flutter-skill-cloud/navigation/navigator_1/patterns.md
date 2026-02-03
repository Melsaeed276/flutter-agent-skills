# Skill: Navigator 1.0 Patterns (Typed Routes)

## Purpose
These patterns reduce fragility in Navigator 1.0 apps by centralizing route names, arguments, and navigation helpers.

## When to use
- You maintain a Navigator 1.0 app.
- You want safer argument passing.

## When NOT to use
- If you are already migrating to go_router, prefer adding routes there.

## Core concepts
- **Typed arguments**: avoid raw `Map`.
- **Route builders**: centralized.

## Recommended patterns
- Create a typed arguments class per route.
- Provide a helper method to push the route.
- Validate arguments and show an error page for invalid input.

## Minimal example

Typed route arguments:

```dart
class DetailsArgs {
  final String id;
  const DetailsArgs(this.id);
}

void goToDetails(BuildContext context, String id) {
  Navigator.of(context).pushNamed('/details', arguments: DetailsArgs(id));
}
```

## Edge cases
- Arguments from deep links may arrive as strings; validate.

## Common mistakes
- Using `settings.arguments as Map` without checks.

## Testing strategy
- Widget test route creation and argument parsing.

## Related skills
- [Navigator pitfalls](./pitfalls.md)
- [Parameters in go_router](../go_router/parameters.md)
- [Error modeling](../../architecture/error_modeling.md)
