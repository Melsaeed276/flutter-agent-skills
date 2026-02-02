# Background Tasks

## Mental model

Background execution is constrained and platform-dependent. Design for partial success and retries.

## Patterns

- Keep tasks idempotent.
- Persist minimal state needed to resume work.

## Pitfalls

- Assuming long-running work will complete uninterrupted.

