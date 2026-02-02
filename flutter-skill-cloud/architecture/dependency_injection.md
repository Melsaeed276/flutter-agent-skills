# Dependency Injection

## Mental model

DI centralizes object construction so you can swap implementations (tests, environments).

## Patterns

- Keep constructors explicit; inject dependencies rather than using globals.
- Prefer a small composition root (app entry point).

## Pitfalls

- Service locator used everywhere hides dependencies and complicates testing.

