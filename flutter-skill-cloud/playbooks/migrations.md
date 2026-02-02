# Migrations Playbook

## Goal

Move from old to new with minimal downtime and clear rollback.

## Approach

- Prefer a “strangler” migration: run old and new in parallel behind an interface.
- Add metrics or logging to compare old vs new outputs.
- Ship behind a feature flag when feasible.

## Common migrations

- Navigation: `Navigator 1.0` → `go_router` ([navigation/SKILL.md](../navigation/SKILL.md))
- State: ad-hoc state → structured async state ([state/shared/async_state.md](../state/shared/async_state.md))
- Serialization: hand-written parsing → mappers ([data/serialization/mappers.md](../data/serialization/mappers.md))

## Rollback plan

- Preserve the old entry point until new behavior is proven.
- Keep data models backward compatible (tolerant readers).
- Document “how to revert” in the PR description.

