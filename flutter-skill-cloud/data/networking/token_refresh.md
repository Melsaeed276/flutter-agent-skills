# Token Refresh

## Mental model

Token refresh is a concurrency problem: many requests can fail at once, but refresh should happen once.

## Patterns

- Gate refresh with a single in-flight refresh future.
- Queue or retry requests after refresh succeeds; fail fast when it doesn’t.

## Pitfalls

- Infinite loops when refresh also returns 401.
- Refresh racing with logout.

