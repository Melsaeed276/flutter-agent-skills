# Networking with Dio

## Patterns

- Wrap Dio in a small client interface so the rest of the app doesn’t depend on Dio directly.
- Centralize base URL, headers, timeouts, and retry policy.

## Pitfalls

- Spreading Dio configuration across many call sites.

## See also

- Interceptors: interceptors.md
- Error modeling: ../../architecture/error_modeling.md

