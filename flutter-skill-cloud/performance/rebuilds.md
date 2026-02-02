# Rebuilds

## Mental model

Rebuilds are normal; expensive rebuilds are the problem. Shrink the rebuild scope.

## Patterns

- Use `const` where possible.
- Move state down near consumers.
- Split widgets to isolate rebuild boundaries.

## Pitfalls

- Watching broad state at the top of the tree.

## See also

- Keys: ../flutter_core/keys.md

