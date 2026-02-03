# Skill: Dart Extensions (Ergonomics Without Coupling)

## Purpose
Extensions let you add small convenience APIs without inheritance or wrappers. They improve readability in Flutter code (formatting, context helpers, domain utilities) when used carefully.

## When to use
- You want reusable helpers like `DateTime` formatting or `BuildContext` convenience.
- You want to keep utility code close to the type it operates on.

## When NOT to use
- Avoid extensions that hide heavy work or side effects.
- Avoid ambiguous names that collide with other packages.

## Core concepts
- **Static dispatch**: extensions are resolved at compile time.
- **Name collisions**: two extensions can define the same member.
- **Scope**: imports control which extensions are visible.

## Recommended patterns
- Keep extensions small and pure.
- Name extensions with a clear suffix: `X` or a domain prefix.
- Prefer free functions for complex operations.
- Avoid adding "business logic" on Flutter types.

## Minimal example

A safe `BuildContext` helper:

```dart
import 'package:flutter/material.dart';

extension BuildContextX on BuildContext {
  void showSnack(String message) {
    ScaffoldMessenger.of(this).showSnackBar(
      SnackBar(content: Text(message)),
    );
  }

  TextTheme get textTheme => Theme.of(this).textTheme;
}
```

## Edge cases
- If two extensions define `textTheme`, imports can become fragile.
- Extensions cannot access private members from other libraries.

## Common mistakes
- Using extensions to smuggle global state.
- Adding async/side effects where call sites look "simple".

## Testing strategy
- Unit test pure extensions.
- For UI helpers, prefer widget tests (snackbars, themes).

## Related skills
- [Theming foundations](../flutter_core/theming_foundations.md)
- [BuildContext](../flutter_core/build_context.md)
- [Design system](../ui/design_system.md)
