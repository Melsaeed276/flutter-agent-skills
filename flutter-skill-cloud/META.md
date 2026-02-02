# META (Global Conventions)

This file defines the rules for authoring and evolving this repository.

## Markdown style rules

- Use `#` for title, `##` for main sections, `###` for subsections.
- Prefer short paragraphs and bullet lists; keep scanning easy.
- Use fenced code blocks with language tags (`dart`, `yaml`, `json`, `text`).
- Avoid screenshots unless the text can’t reasonably explain it.

## Naming conventions

- Hubs are named `SKILL.md` and live at a domain root (for example `ui/SKILL.md`).
- Topic files are lowercase with underscores: `layout_constraints.md`.
- Keep file names stable once linked from other docs.

## Code snippet conventions

- Snippets should be minimal and runnable-in-spirit (even if not a full app).
- Prefer `// ...` to omit irrelevant parts.
- Show both “do” and “avoid” only when it clarifies a common pitfall.

## Error-handling philosophy (for examples)

- Model errors as data (typed failures) where it improves UX and testing.
- Prefer predictable behavior over “try/catch everywhere”.
- Surface user-facing errors with actionable messages; log diagnostic context separately.

## Keeping files small

- Target: under ~200 lines per file.
- Split when a file starts mixing multiple concerns (for example “responsive” vs “foldables”).
- Prefer linking to a dedicated subtopic rather than expanding a hub.

## No secrets rule

Never include:

- API tokens/keys, credentials, private endpoints, internal hostnames.
- Real customer data or identifiers.

If you need placeholders, use obvious fakes like `https://example.com` and `YOUR_API_KEY_HERE`.

## Portability rules

- Do not reference specific editors, UI buttons, or proprietary agent features.
- Assume only a Git repo + Markdown reader.
- Prefer general steps (“run tests”, “check logs”) over tool-specific commands.

