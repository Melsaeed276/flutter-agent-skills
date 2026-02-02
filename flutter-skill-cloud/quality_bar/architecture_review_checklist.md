# Architecture Review Checklist

## Checklist

- [ ] Clear boundaries: UI ↔ state ↔ domain ↔ data.
- [ ] Dependencies point inward (UI depends on abstractions, not concretes).
- [ ] Errors are modeled consistently ([../architecture/error_modeling.md](../architecture/error_modeling.md)).
- [ ] Side effects are isolated and testable.
- [ ] Feature folder structure is consistent across the app.
- [ ] Migration plan exists for breaking changes.

## See also

- [../architecture/SKILL.md](../architecture/SKILL.md)
- [../playbooks/refactoring.md](../playbooks/refactoring.md)

