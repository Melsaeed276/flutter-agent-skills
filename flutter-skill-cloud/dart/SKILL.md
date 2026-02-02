# Dart Skills

## What this domain covers

Dart language fundamentals that directly affect Flutter code: async behavior, null safety, collections, isolates, extensions, and error handling.

## When to read it

- You’re debugging async race conditions, cancellations, or “setState after dispose”.
- You’re refactoring APIs and need safer types and nullability.
- You need to move CPU-heavy work off the UI thread.

## Subtopics

- Async fundamentals: [async.md](./async.md)
- Null safety: [null_safety.md](./null_safety.md)
- Collections & immutability: [collections.md](./collections.md)
- Extensions: [extensions.md](./extensions.md)
- Isolates: [isolates.md](./isolates.md)
- Error handling: [error_handling.md](./error_handling.md)

## Decision guide

- If you need **structured async flows**, go to [async.md](./async.md).
- If you need **safe APIs and fewer runtime null crashes**, go to [null_safety.md](./null_safety.md).
- If you need **performance for CPU work**, go to [isolates.md](./isolates.md).
- If you need **consistent failures and retries**, go to [error_handling.md](./error_handling.md).

