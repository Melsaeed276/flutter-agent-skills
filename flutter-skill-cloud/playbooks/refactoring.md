# Refactoring Playbook

## Goal

Improve structure without changing behavior.

## When to read

- You’re about to reorganize folders, split widgets, or introduce a new architecture layer.
- The team wants consistency across features.

## Safe refactor steps

- Define “done” first ([quality_bar/definition_of_done.md](../quality_bar/definition_of_done.md)).
- Add tests around current behavior ([testing/SKILL.md](../testing/SKILL.md)).
- Refactor in small, reviewable commits: rename → extract → redirect → delete.
- Keep public APIs stable (routes, repositories, DTOs) until the end.

## Common refactors

- “God widget” → extract layout vs state vs side effects.
- “Repository does too much” → split networking vs mapping vs caching.
- “State explosion” → model states and transitions ([state/shared/state_modeling.md](../state/shared/state_modeling.md)).

