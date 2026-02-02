# App Lifecycle

## Mental model

Apps move through states: foreground/background, inactive, resumed, detached. Treat lifecycle as an input to state.

## Patterns

- Pause/resume subscriptions appropriately.
- Persist drafts or critical work on background transitions.

## Pitfalls

- Losing in-progress edits when the OS kills the app.

## See also

- Widget lifecycle: ../flutter_core/widget_lifecycle.md

