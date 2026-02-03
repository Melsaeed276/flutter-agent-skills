# META (Global Conventions)

This file defines the repository-wide rules for authoring, portability, and maintenance.

## Purpose

This repo is a "skills" library: small, focused Markdown pages that teach a single topic well.
The goal is fast retrieval and reliable application in real Flutter/Dart projects.

## When to use

- You want consistent docs that work for both editor agents and cloud agents.
- You want patterns + minimal examples + pitfalls + tests in one place.

## When NOT to use

- Do not store private/internal knowledge here (tokens, endpoints, customer data).
- Do not use this as a full tutorial series; keep docs small and link out.

## Core concepts

- **Single-topic pages**: each doc should answer one kind of question.
- **Progressive disclosure**: hubs route to leaf docs; leaf docs include links to adjacent topics.
- **Portability**: no UI instructions tied to a specific tool.

## Recommended patterns

- Use headings consistently (see [templates/SKILL_TEMPLATE.md](./templates/SKILL_TEMPLATE.md)).
- Prefer short paragraphs and compact bullet lists.
- Use fenced code blocks with language tags: `dart`, `yaml`, `json`, `text`.
- Examples should be "runnable-in-spirit": compile with small adjustments.

## Minimal example

A good doc pattern:

```text
- Define the mental model.
- Show a minimal snippet.
- List common mistakes.
- Show a testing approach.
```

## Edge cases

- If an API is unstable or version-sensitive, describe how to verify it.
- If behavior differs by platform (iOS vs Android vs web), call it out.

## Common mistakes

- Copying large blocks from official docs.
- Adding long, unstructured notes instead of a reusable pattern.
- Using non-portable file paths or editor steps.

## Testing strategy

- Mention the *lowest-cost* test that provides confidence:
  - Pure logic -> unit tests.
  - UI wiring -> widget tests.
  - Cross-screen flows -> integration tests.
- Prefer deterministic tests: fake clocks, fake repositories, stable keys.

## Related skills

- Router: [SKILL_INDEX.md](./SKILL_INDEX.md)
- Templates: [templates/SKILL_TEMPLATE.md](./templates/SKILL_TEMPLATE.md)
