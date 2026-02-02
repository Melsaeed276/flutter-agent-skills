# Isolates

## Mental model

- The UI runs on the main isolate; heavy CPU work causes jank.
- Isolates don’t share memory; communicate by messages.

## Patterns

- Use `compute` for simple pure functions and moderate payloads.
- For long-lived work, create a dedicated isolate and reuse it.

## Pitfalls

- Passing huge objects is expensive; serialize minimal data.
- Many small isolate spawns can be worse than a single optimized algorithm.

## Example (compute)

```dart
import 'package:flutter/foundation.dart';

int expensiveSum(List<int> values) => values.fold(0, (a, b) => a + b);

Future<int> sumOffThread(List<int> values) => compute(expensiveSum, values);
```

## See also

- Performance jank: ../performance/jank.md
- Flutter rendering: ../flutter_core/rendering_pipeline.md

