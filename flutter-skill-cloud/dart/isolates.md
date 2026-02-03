# Skill: Dart Isolates (Off-Main-Thread Work)

## Purpose
Flutter UI runs on a single thread. CPU-heavy work (parsing large JSON, image processing, sorting big lists) can cause jank.
Isolates provide concurrency via message passing and are the primary tool for keeping the UI thread responsive.

## When to use
- Frame drops happen during parsing/processing.
- Work is CPU-bound (not I/O bound).
- You need to run expensive transforms without blocking the UI.

## When NOT to use
- Do not use isolates for network I/O; async I/O does not block the UI thread.
- Do not spawn isolates for tiny work; overhead can dominate.

## Core concepts
- **No shared memory**: isolate communication uses message passing.
- **Transferable data**: messages should be simple/serializable.
- **Granularity**: batch work to amortize overhead.

## Recommended patterns
- For one-off CPU work, use `Isolate.run` (Dart) or `compute` (Flutter).
- Keep isolate entrypoints top-level/static.
- Avoid capturing large object graphs.
- Measure: move only the bottleneck.

## Minimal example

Using `Isolate.run` for a CPU-heavy transform:

```dart
import 'dart:isolate';

Future<List<int>> sortBigList(List<int> values) {
  // Copy before sending if the caller might mutate.
  final input = List<int>.from(values);
  return Isolate.run(() {
    input.sort();
    return input;
  });
}
```

## Edge cases
- Some objects are not sendable across isolates.
- If you need streaming results, you may need a long-lived isolate and ports.

## Common mistakes
- Spawning isolates for small work in tight loops.
- Sending large, deeply nested objects and paying serialization cost.

## Testing strategy
- Unit test correctness of the transform.
- Add a performance smoke test for large inputs (time bound).

## Related skills
- [Performance: Jank](../performance/jank.md)
- [Performance: Isolates](../performance/isolates.md)
- [Async fundamentals](./async.md)
