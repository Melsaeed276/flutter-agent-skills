# Skill: BuildContext (Scope, Timing, and Ownership)

## Purpose
`BuildContext` is a handle to a location in the widget tree. Many Flutter issues come from using the wrong context (wrong scope) or using it at the wrong time (before the tree is ready or after disposal).

## When to use
- You get errors like "Looking up a deactivated widget's ancestor".
- Snackbars/dialogs/navigators/theme lookups fail or use the wrong ancestor.
- You need to safely use context after `await`.

## When NOT to use
- Do not store `BuildContext` long-term; store IDs, callbacks, or use state management.
- Do not use context to access business logic that should be injected.

## Core concepts
- **Scope**: `Theme.of(context)` finds the nearest ancestor `Theme`.
- **Timing**: some lookups require the first frame (`initState` vs `didChangeDependencies`).
- **Mounted**: after disposal, context should not be used.

## Recommended patterns
- Prefer `didChangeDependencies` for work that depends on inherited widgets.
- Use `WidgetsBinding.instance.addPostFrameCallback` for one-time UI side effects.
- After `await`, check `mounted` (or `context.mounted`) before using context.
- Use `Builder` to create a context under a specific ancestor (e.g., `Scaffold`).

## Minimal example

Safe post-frame side effect:

```dart
import 'package:flutter/material.dart';

class WelcomeBanner extends StatefulWidget {
  const WelcomeBanner({super.key});

  @override
  State<WelcomeBanner> createState() => _WelcomeBannerState();
}

class _WelcomeBannerState extends State<WelcomeBanner> {
  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addPostFrameCallback((_) {
      if (!mounted) return;
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('Welcome!')),
      );
    });
  }

  @override
  Widget build(BuildContext context) {
    return const SizedBox.shrink();
  }
}
```

## Edge cases
- Nested `Navigator`s: `Navigator.of(context)` may not be the one you expect.
- Modals/overlays: the overlay context can differ from page context.

## Common mistakes
- Calling `showDialog` in `initState` directly.
- Using context after navigation pops the route.

## Testing strategy
- Widget test: pump widget, trigger async, ensure no exceptions when disposed.
- Widget test: ensure snackbars/dialogs appear under the right scaffold.

## Related skills
- [Widget lifecycle](./widget_lifecycle.md)
- [Navigation pitfalls](../navigation/navigator_1/pitfalls.md)
- [State async patterns](../state/shared/async_state.md)
