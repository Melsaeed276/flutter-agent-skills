# Performance Checklist

## Checklist

- [ ] Rebuild scope is minimal (state near consumers; `const` where possible).
- [ ] Lists are virtualized and item widgets are cheap.
- [ ] Images are sized/decoded appropriately ([../performance/images.md](../performance/images.md)).
- [ ] Expensive work is moved off the UI thread when needed ([../dart/isolates.md](../dart/isolates.md)).
- [ ] Animations avoid layout thrash and overdraw.
- [ ] Verified on low-end device class and large-screen class.

## See also

- [../performance/SKILL.md](../performance/SKILL.md)
- [../performance/jank.md](../performance/jank.md)

