# Skill: Widget Lifecycle (State, Subscriptions, Disposal)

## Purpose
Lifecycle correctness prevents memory leaks, duplicate subscriptions, and async work updating dead widgets.
This doc describes how to use the `State` lifecycle methods safely.

## When to use
- You manage controllers (animation, scroll, text) or stream subscriptions.
- A widget responds to changes in `widget` parameters.
- Async work needs cancellation/cleanup.

## When NOT to use
- Do not put business logic in lifecycle methods; call injected services/use-cases.
- Do not rely on lifecycle ordering for correctness; encode invariants in types.

## Core concepts
- **initState**: initialize controllers; no inherited lookups that depend on context.
- **didChangeDependencies**: respond to inherited widget changes.
- **didUpdateWidget**: respond to new configuration.
- **dispose**: cancel subscriptions, dispose controllers.

## Recommended patterns
- Create controllers in `initState`, dispose them in `dispose`.
- Use `didUpdateWidget` to update controllers when inputs change.
- Guard async continuations with `mounted`.

## Minimal example

A controller + subscription lifecycle:

```dart
import 'dart:async';
import 'package:flutter/material.dart';

class TickLabel extends StatefulWidget {
  final Duration interval;
  const TickLabel({super.key, required this.interval});

  @override
  State<TickLabel> createState() => _TickLabelState();
}

class _TickLabelState extends State<TickLabel> {
  Timer? _timer;
  int _count = 0;

  @override
  void initState() {
    super.initState();
    _startTimer();
  }

  @override
  void didUpdateWidget(covariant TickLabel oldWidget) {
    super.didUpdateWidget(oldWidget);
    if (oldWidget.interval != widget.interval) {
      _startTimer();
    }
  }

  void _startTimer() {
    _timer?.cancel();
    _timer = Timer.periodic(widget.interval, (_) {
      if (!mounted) return;
      setState(() => _count++);
    });
  }

  @override
  void dispose() {
    _timer?.cancel();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) => Text('Ticks: $_count');
}
```

## Edge cases
- `didChangeDependencies` can be called more than once.
- `dispose` can be triggered during async work; always guard continuations.

## Common mistakes
- Forgetting to dispose controllers/subscriptions.
- Starting timers/streams multiple times (duplicate work).

## Testing strategy
- Widget test: pump, advance time, verify UI updates; dispose and verify no exceptions.

## Related skills
- [Dart async](../dart/async.md)
- [Performance: Memory](../performance/memory.md)
- [Platform lifecycle](../platform/app_lifecycle.md)
