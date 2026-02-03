# Skill: Deep Links (Mobile + Web URLs)

## Purpose
Deep links allow external entry into your app (emails, push notifications, web URLs). They require robust parameter validation and safe initialization.

## When to use
- You need to open screens from URLs.
- You support web/desktop.
- You integrate notifications that open routes.

## When NOT to use
- Do not rely on in-memory `extra` for deep-link-required data.

## Core concepts
- **Initial location**: the first route for app start.
- **Cold vs warm start**: app launched vs already running.
- **Validation**: deep links can be malformed.

## Recommended patterns
- Put required IDs in the URL and fetch data.
- Validate parameters and show a friendly error page.
- Keep deep link handling idempotent.

## Minimal example

Route that supports deep link entry:

```dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';

final router = GoRouter(
  routes: [
    GoRoute(
      path: '/order/:orderId',
      builder: (context, state) {
        final id = state.pathParameters['orderId'] ?? '';
        if (id.isEmpty) {
          return const Scaffold(body: Text('Invalid order link'));
        }
        return OrderScreen(orderId: id);
      },
    ),
  ],
);

class OrderScreen extends StatelessWidget {
  final String orderId;
  const OrderScreen({super.key, required this.orderId});
  @override
  Widget build(context) => Scaffold(body: Text('Order $orderId'));
}
```

## Edge cases
- Links opened while app is running can collide with ongoing flows; decide whether to interrupt.
- Some screens require auth; coordinate with guards.

## Common mistakes
- Crashing on missing/invalid params.
- Assuming deep links always have network connectivity.

## Testing strategy
- Integration test deep link entry for logged-in and logged-out.
- Widget test invalid link rendering.

## Related skills
- [Guards](./guards.md)
- [Push notifications](../../platform/push_notifications.md)
- [Integration tests](../../testing/integration_tests.md)
