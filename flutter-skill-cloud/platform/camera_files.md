# Camera & Files

## Patterns

- Separate capture/pick from processing; move heavy processing off the UI thread.
- Handle permissions and error states explicitly.

## Pitfalls

- Large image decoding on main isolate leading to jank.

## See also

- Images performance: ../performance/images.md
- Isolates: ../dart/isolates.md

