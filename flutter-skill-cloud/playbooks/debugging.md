# Skill: Debugging Flutter/Dart Issues

## Purpose
This playbook provides a repeatable debugging loop for Flutter apps: reproduce, localize, instrument, fix, and lock in with tests.
It is designed to work across device classes (phone/tablet/foldable) and platforms (iOS/Android/web/desktop).

## When to use
- A bug is reported but reproduction steps are unclear.
- A regression appears after a refactor or dependency update.
- You see crashes, infinite spinners, auth loops, navigation glitches, or layout overflows.

## When NOT to use
- You already have a minimal repro and a clear root cause; go straight to the relevant skill doc.
- The issue is purely product/requirements ambiguity (not technical).

## Core concepts
- **Repro first**: debugging without reproduction is guessing.
- **Binary search**: reduce the search space by isolating variables.
- **Make state observable**: logs, asserts, DevTools, and instrumentation.
- **Stop conditions**: know when to stop digging and change approach.

## Recommended patterns
- Start with the smallest failing scenario; write it down as steps.
- Prefer deterministic reproduction (seeded data, fixed clocks, stubs).
- Add temporary instrumentation (logs, `assert`, `debugPrint`, timeline events).
- Localize by layers: UI -> state -> domain -> data -> platform.
- After fix: add a regression test and remove temporary logs.

## Minimal example

Debug loop (copy/paste checklist):

```text
1) Reproduce: device + build mode + steps + expected vs actual.
2) Localize: which layer (UI/state/data/platform)?
3) Observe: add logs/asserts + capture stack traces.
4) Minimize: reduce code path until the bug still happens.
5) Fix: implement smallest change.
6) Verify: rerun repro + add regression test.
7) Clean: remove debug code; document root cause.
```

## Edge cases
- Release-only bugs: reproduce in `--release` or profile mode, and watch for timing differences.
- Async/lifecycle: bugs that disappear when you add logs are often races; see [dart/async.md](../dart/async.md) and [platform/app_lifecycle.md](../platform/app_lifecycle.md).
- Multi-navigator apps: using the wrong `BuildContext` can route to the wrong navigator.
- Foldables: posture changes can re-layout and expose hidden state assumptions.

## Common mistakes
- Changing multiple variables at once (device + code + dependency) and losing signal.
- Debugging UI symptoms when the bug is in state/data invariants.
- Leaving instrumentation in production code.

## Testing strategy
- Convert the minimal repro into:
  - Unit tests for pure logic.
  - Widget tests for UI/state wiring.
  - Integration tests for end-to-end flows (routing/auth).

## Related skills
- [Performance: DevTools](../performance/devtools.md)
- [Flutter core: Layout constraints](../flutter_core/layout_constraints.md)
- [State: Async state](../state/shared/async_state.md)
- [Navigation testing](../navigation/go_router/testing.md)
