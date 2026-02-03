# Skill: go_router Overview (Declarative Routing)

## Purpose
go_router is a declarative router for Flutter that supports deep links, web URLs, redirects, and nested navigation.
This doc provides the mental model and common building blocks.

## When to use
- You need deep linking or web URL-based navigation.
- You need auth guards/redirects.
- You have nested navigation (tabs, shell).

## When NOT to use
- For tiny apps with no deep links, Navigator 1.0 can be simpler.

## Core concepts
- **GoRouter**: top-level router configuration.
- **GoRoute**: a path pattern -> page.
- **redirect**: navigation guard decision.
- **ShellRoute**: nested navigation scaffolding.

## Recommended patterns
- Keep route definitions centralized.
- Parse parameters at the boundary; keep pages typed.
- Prefer `goNamed`/named routes for refactors.

## Minimal example

A minimal router:

```dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';

final router = GoRouter(
  routes: [
    GoRoute(
      path: '/',
      builder: (context, state) => const HomeScreen(),
      routes: [
        GoRoute(
          path: 'settings',
          builder: (context, state) => const SettingsScreen(),
        ),
      ],
    ),
  ],
);

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(routerConfig: router);
  }
}

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: ElevatedButton(
          onPressed: () => context.go('/settings'),
          child: const Text('Settings'),
        ),
      ),
    );
  }
}

class SettingsScreen extends StatelessWidget {
  const SettingsScreen({super.key});

  @override
  Widget build(BuildContext context) => const Scaffold(body: Text('Settings'));
}
```

## Edge cases
- Route builders can be called often; keep them cheap.
- State restoration/back stack differ by platform; test on web and mobile.

## Common mistakes
- Using raw strings everywhere; prefer named routes.
- Creating redirect loops when auth state changes.

## Testing strategy
- Widget test router config with `MaterialApp.router`.
- Integration test deep links.

## Related skills
- [Setup](./setup.md)
- [Deep links](./deep_links.md)
- [Testing](./testing.md)
