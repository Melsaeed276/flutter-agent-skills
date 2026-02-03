# Skill: go_router Parameters (Path, Query, Extras)

## Purpose
Parameter handling is a common source of bugs (wrong types, missing keys, encoding issues).
This doc shows safe patterns for parsing path and query parameters.

## When to use
- You need typed IDs from the URL.
- You need query params for filters/sorts.
- You need to pass complex objects between routes.

## When NOT to use
- Avoid passing large objects via `extra` when a repository lookup by ID is better.

## Core concepts
- **Path params**: `/product/:id`.
- **Query params**: `?tab=reviews`.
- **extra**: in-memory data; not durable for deep links.

## Recommended patterns
- Parse and validate at the boundary; show an error if invalid.
- Prefer IDs in the URL; fetch full objects.
- Treat query params as optional and provide defaults.

## Minimal example

Typed path parameter parsing:

```dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';

final router = GoRouter(
  routes: [
    GoRoute(
      path: '/product/:id',
      builder: (context, state) {
        final id = state.pathParameters['id'];
        if (id == null || id.isEmpty) {
          return const Scaffold(body: Text('Missing id'));
        }
        return ProductScreen(productId: id);
      },
    ),
  ],
);

class ProductScreen extends StatelessWidget {
  final String productId;
  const ProductScreen({super.key, required this.productId});

  @override
  Widget build(BuildContext context) => Scaffold(body: Text('Product $productId'));
}
```

## Edge cases
- Deep links: `extra` will be null; do not rely on it.
- Query param encoding: spaces and special characters need encoding.

## Common mistakes
- Force unwrapping missing params.
- Using `extra` for required navigation state.

## Testing strategy
- Widget test: invalid parameter shows error UI.

## Related skills
- [Deep links](./deep_links.md)
- [Guards](./guards.md)
- [Error modeling](../../architecture/error_modeling.md)
