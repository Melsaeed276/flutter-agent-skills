# Skill: go_router Guards (Redirects and Auth)

## Purpose
Guards enforce access control and flow rules (login required, onboarding complete).
This doc focuses on redirects that are correct, loop-free, and testable.

## When to use
- Some routes require authentication.
- You need onboarding/paywall routing.
- You need to prevent access based on feature flags or roles.

## When NOT to use
- Do not fetch from network in redirects.
- Do not put business logic in redirect; call a dependency that exposes a small decision.

## Core concepts
- **redirect**: returns a string location or null.
- **refreshListenable**: triggers redirect reevaluation when auth state changes.
- **Loop prevention**: ensure each redirect moves toward a stable route.

## Recommended patterns
- Keep redirect synchronous and pure.
- Encode redirect rules as a small decision function and unit test it.
- Preserve the intended destination via a query parameter.

## Minimal example

A simple login guard:

```dart
import 'package:go_router/go_router.dart';

bool isLoggedIn() => false; // replace with state

final router = GoRouter(
  routes: [
    GoRoute(path: '/login', builder: (_, __) => const LoginScreen()),
    GoRoute(path: '/home', builder: (_, __) => const HomeScreen()),
  ],
  redirect: (context, state) {
    final loggingIn = state.matchedLocation == '/login';
    if (!isLoggedIn() && !loggingIn) return '/login?from=${state.uri}';
    if (isLoggedIn() && loggingIn) return '/home';
    return null;
  },
);

class LoginScreen extends StatelessWidget {
  const LoginScreen({super.key});
  @override
  Widget build(context) => const SizedBox.shrink();
}

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});
  @override
  Widget build(context) => const SizedBox.shrink();
}
```

## Edge cases
- Auth refresh: transient "unknown" auth state should not bounce users.
- Deep links: preserve and restore the requested path.

## Common mistakes
- Redirect loops when login page also triggers guard.
- Redirecting on every rebuild due to unstable auth signal.

## Testing strategy
- Unit test the redirect decision function.
- Integration test: deep link to protected route while logged out.

## Related skills
- [Async state](../../state/shared/async_state.md)
- [Token refresh](../../data/networking/token_refresh.md)
- [go_router testing](./testing.md)
