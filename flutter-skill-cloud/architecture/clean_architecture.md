# Clean Architecture (Practical)

## Mental model

- UI depends on abstractions (interfaces), not concretes.
- Data layer implements those abstractions.
- Domain policies stay free of Flutter details.

## Patterns

- Keep dependency direction one-way.
- Use simple boundaries; don’t add layers unless they remove complexity.

## Pitfalls

- Over-engineering: too many layers for a small app.

