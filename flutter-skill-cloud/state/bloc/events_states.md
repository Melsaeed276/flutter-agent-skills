# BLoC Events & States

## Patterns

- Keep events user-intent focused (not “set field X to Y” unless needed).
- Keep states render-focused (what the UI needs).
- Model errors and retries explicitly.

## Pitfalls

- Large states that include derived UI formatting.

