# Skill: Testing go_router (Widget + Integration)

## Purpose
Routing bugs are often only visible end-to-end. This doc provides a pragmatic testing strategy that covers configuration, redirects, and deep links.

## When to use
- You are adding routes or redirects.
- You are implementing deep links.
- You saw a back stack regression.

## When NOT to use
- Do not test go_router internals; test your app behavior.

## Core concepts
- **Widget tests**: validate router config and UI outcomes.
- **Integration tests**: validate platform navigation and deep links.
- **Redirect determinism**: redirect decisions should be testable.

## Recommended patterns
- Widget-test critical route entry points with `MaterialApp.router`.
- Unit-test your redirect decision function.
- Add at least one integration test that covers auth + deep link.

## Minimal example

Widget test shape:

```dart
// Pump MaterialApp.router(routerConfig: router)
// Navigate by setting router location or simulating taps.
// Expect specific screen widgets.
```

## Edge cases
- Async guards: avoid async in redirects; otherwise tests become flaky.
- Nested navigators: back behavior needs integration coverage.

## Common mistakes
- Only manual testing; regressions slip in.
- Testing with fake URLs that don't match real deep link patterns.

## Testing strategy
- Widget tests for:
  - basic routes
  - invalid parameters
  - errorBuilder
- Integration tests for:
  - deep link entry
  - back navigation
  - auth guard flow

## Related skills
- [Integration tests](../../testing/integration_tests.md)
- [Guards](./guards.md)
- [Deep links](./deep_links.md)
