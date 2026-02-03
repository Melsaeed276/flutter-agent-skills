# Skill: BLoC Side Effects (Navigation, Toasts, One-Off Events)

## Purpose
State should be a snapshot. Side effects (navigation, snackbars, analytics) are one-off actions that should not be re-triggered by rebuilds.
This doc describes patterns for modeling and handling effects.

## When to use
- You need to show a toast/snackbar after an event.
- You need to navigate after success/failure.

## When NOT to use
- Do not represent one-off effects as persistent state fields.

## Core concepts
- **Effect**: one-time signal.
- **Listener**: UI layer reacts to effects.
- **Idempotency**: rebuilds should not replay effects.

## Recommended patterns
- Use listeners (`BlocListener` or equivalent) for effects.
- Emit a distinct state that implies an effect only when it is safe, then immediately transition.
- Prefer explicit effect streams when complexity grows.

## Minimal example

Effect handling strategy:

```text
- BLoC emits a success state.
- UI listener shows snackbar and triggers navigation.
- BLoC transitions to a stable state so the effect isn't replayed.
```

## Edge cases
- Back navigation: ensure effects don't fire when leaving the screen.
- Duplicate submissions: disable button or dedupe commands.

## Common mistakes
- Triggering navigation in `build`.
- Storing a `BuildContext` inside the BLoC.

## Testing strategy
- Test that the effect signal occurs once per event.
- Widget test that listeners trigger the expected UI action.

## Related skills
- [BuildContext timing](../../flutter_core/build_context.md)
- [Navigation testing](../../navigation/go_router/testing.md)
- [Widget tests](../../testing/widget_tests.md)
