# Interceptors

## Mental model

Interceptors are cross-cutting policies: headers, auth, logging, retries, and error normalization.

## Patterns

- Keep interceptor responsibilities narrow and ordered.
- Normalize errors into a small set of failure categories.

## Pitfalls

- Logging sensitive data (never log tokens or PII).
- Retrying non-idempotent requests without care.

