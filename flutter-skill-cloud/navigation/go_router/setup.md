# Skill: go_router Setup (RouterConfig, Observability)

## Purpose
Router setup is where you wire error pages, observers, and state-driven redirects.
This doc focuses on a maintainable setup and where to put dependencies.

## When to use
- You are introducing go_router.
- You need centralized error handling and redirects.
- You want observability (logging/analytics) for route changes.

## When NOT to use
- Do not build the router inside a frequently rebuilding widget without memoization.

## Core concepts
- **routerConfig**: passed to `MaterialApp.router`.
- **refreshListenable**: triggers redirect evaluation on state changes.
- **errorBuilder**: fallback route errors.

## Recommended patterns
- Build the router once (top-level or via DI) and inject dependencies.
- Keep redirect logic pure and fast.
- Add route logging via observers (where supported).

## Minimal example

Router with an error page:

```dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';

GoRouter buildRouter() {
  return GoRouter(
    routes: [
      GoRoute(path: '/', builder: (_, __) => const Home()),
    ],
    errorBuilder: (context, state) {
      return Scaffold(
        body: Center(child: Text(state.error.toString())),
      );
    },
  );
}

class Home extends StatelessWidget {
  const Home({super.key});
  @override
  Widget build(BuildContext context) => const Scaffold(body: Text('Home'));
}
```

## Edge cases
- Redirect evaluation can run often; avoid async work inside redirect.
- Web: ensure unknown paths show a useful error page.

## Common mistakes
- Calling `setState` from redirect.
- Doing network calls in redirect.

## Testing strategy
- Widget test: unknown route shows errorBuilder.

## Related skills
- [Guards](./guards.md)
- [Deep links](./deep_links.md)
- [CI testing](../../testing/ci_testing.md)
