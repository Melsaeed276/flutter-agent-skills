# Skill: Navigator 1.0 Pitfalls (Context, Back Stack, Races)

## Purpose
Navigator 1.0 is simple but easy to misuse when async operations and nested navigators enter the picture.
This doc highlights common pitfalls and how to avoid them.

## When to use
- You see crashes after navigation.
- Back button behavior is inconsistent.
- Navigation triggers during async operations.

## When NOT to use
- Do not patch around deep link and guard requirements; consider migrating to go_router.

## Core concepts
- **Context validity**: after a route pops, some contexts are invalid.
- **Re-entrancy**: multiple navigation calls can interleave.
- **Nested navigators**: dialogs, bottom sheets, and tabs.

## Recommended patterns
- Guard navigation after `await` with `mounted`.
- Serialize navigation actions (disable buttons, dedupe).
- Use the correct navigator (root vs nested) intentionally.

## Minimal example

Safe navigation after async:

```dart
Future<void> saveAndClose(BuildContext context) async {
  await Future<void>.delayed(const Duration(milliseconds: 10));
  if (!context.mounted) return;
  Navigator.of(context).pop();
}
```

## Edge cases
- Double taps can push the same route twice.
- Popping from the wrong navigator pops the entire shell.

## Common mistakes
- Navigating from within `build`.
- Calling `Navigator.pop` twice (underflow).

## Testing strategy
- Widget test double-tap prevention.
- Integration test back stack for multi-step flows.

## Related skills
- [BuildContext](../../flutter_core/build_context.md)
- [go_router guards](../go_router/guards.md)
- [Integration tests](../../testing/integration_tests.md)
