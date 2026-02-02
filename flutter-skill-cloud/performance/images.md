# Images

## Patterns

- Serve appropriately sized images for each breakpoint (don’t decode huge images for small UI).
- Cache with bounds; prefer predictable eviction.
- Avoid unnecessary image filters and large shadows.

## Pitfalls

- Decoding large images on the main isolate.

## See also

- Isolates: ../dart/isolates.md
- Breakpoints: ../ui/breakpoints.md

