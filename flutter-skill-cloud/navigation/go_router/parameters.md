# go_router Parameters

## Patterns

- Prefer typed parameters in your app layer even if the router receives strings.
- Validate parameters at the boundary and route to an error page when invalid.

## Pitfalls

- Assuming query parameters exist; handle missing/invalid values.

