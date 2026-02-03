# Skill: Navigator 1.0 Overview (Imperative Stack)

## Purpose
Navigator 1.0 uses an imperative stack model (push/pop/replace). It is still common in legacy apps and small projects.
This doc explains the mental model and when it is appropriate.

## When to use
- Small apps without deep links or complex nested routing.
- Legacy codebases.

## When NOT to use
- Apps with deep links and web support are usually better served by a declarative router.

## Core concepts
- **Stack**: pages are pushed and popped.
- **Route**: defines a page transition.
- **onGenerateRoute**: centralized route creation.

## Recommended patterns
- Centralize route names and argument types.
- Prefer typed wrappers over raw `pushNamed` calls everywhere.
- Define a single place for route argument parsing.

## Minimal example

Central route table:

```dart
Route<dynamic> onGenerateRoute(RouteSettings settings) {
  switch (settings.name) {
    case '/':
      return MaterialPageRoute(builder: (_) => const Home());
    default:
      return MaterialPageRoute(builder: (_) => const Unknown());
  }
}
```

## Edge cases
- Deep links require extra plumbing.
- Nested navigators can complicate back behavior.

## Common mistakes
- Passing dynamic maps as arguments without validation.
- Using context after popping.

## Testing strategy
- Widget test `onGenerateRoute` and basic navigation.

## Related skills
- [Navigator patterns](./patterns.md)
- [Navigator pitfalls](./pitfalls.md)
- [go_router overview](../go_router/overview.md)
