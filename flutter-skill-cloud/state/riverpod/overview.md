# Riverpod Overview

## Mental model

Riverpod represents app state as a graph of providers. UI reads providers; providers depend on other providers.

## When it shines

- Dependency injection + state composition.
- Testability via provider overrides.

## Pitfalls

- Putting UI concerns in providers instead of domain/state concerns.

## See also

- Providers: providers.md
- Notifiers: notifiers.md

