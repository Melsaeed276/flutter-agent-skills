# Checklist: <name>

## Purpose
What this checklist verifies and why it matters.

## When to use
- Before merging
- Before releasing

## When NOT to use
- If the change is trivial and does not affect behavior (still run basic checks)

## Core concepts
- **Scope**: what is in/out
- **Signals**: what evidence you collect

## Recommended patterns
- Prefer a short checklist with strong signals.
- Prefer objective checks over opinions.

## Minimal example

```text
[ ] Item written as a verifiable statement.
[ ] Includes a link to evidence (test, screenshot, log) when applicable.
```

## Edge cases
- Large refactors: run the checklist per subsystem.
- Hotfixes: be explicit about what you are skipping and why.

## Common mistakes
- Writing items that are not verifiable.
- Skipping evidence (no tests, no repro).

## Testing strategy
- Add the minimal regression test for the bug that motivated the change.

## Related skills
- [Quality bar](../quality_bar/definition_of_done.md)
