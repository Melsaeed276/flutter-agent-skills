# Theming Foundations

## Mental model

- Theme is inherited data; changes trigger rebuilds where read.
- A design system is easier when tokens are centralized and consistent.

## Patterns

- Use `ThemeData` and `ColorScheme` as the primary “source of truth”.
- Wrap feature-specific themes in subtrees when needed.

## Pitfalls

- Reading theme colors directly everywhere instead of using semantic tokens.

## See also

- Theming tokens: ../ui/theming_tokens.md
- Material 3: ../ui/material3.md

