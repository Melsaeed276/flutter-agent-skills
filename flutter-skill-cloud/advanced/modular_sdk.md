# Modular SDK

## Goal

Share domain and data logic across multiple apps while keeping UI flexible.

## Patterns

- Define stable interfaces and avoid Flutter dependencies in the SDK core.
- Provide extension points for app-specific behavior.

## Pitfalls

- Leaking app-specific assumptions into the shared module.

