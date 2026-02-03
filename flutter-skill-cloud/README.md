# Universal Flutter Skills Cloud

A portable, tool-agnostic knowledge base of small Markdown “skills” for Flutter + Dart.
This repository serves both editor agents (Cursor) and cloud agents (autonomous reviewers, CI copilots), so each doc emphasizes mental models, patterns, minimal examples, and testing guidance without leaking tool-specific instructions or secrets.

## Purpose-driven organization

1. [SKILL_INDEX.md](./SKILL_INDEX.md) is the router: it maps symptoms (jank, overflow, slow tests) to domain hubs.
2. Each domain folder has a `SKILL.md` hub describing its focus and linking to leaf topic docs.
3. Leaf docs (e.g., `ui/responsive.md`, `data/networking/dio.md`) follow the shared template, which includes purpose, examples, edge cases, common mistakes, testing strategy, and related links.

### Core library structure

| Folder | Role |
| --- | --- |
| `dart/` | Language foundations: async, null safety, isolates, extensions, collections, error handling. |
| `flutter_core/` | Engine behaviors: BuildContext, lifecycle, constraints, rendering, theming, keys. |
| `state/` | State modeling, Riverpod + BLoC patterns, shared helpers, testing guidance. |
| `navigation/` | Declarative `go_router` plus legacy Navigator 1.0 guidance. |
| `architecture/` | Feature structure, clean architecture, DI, repositories, error contracts. |
| `data/` | Networking, serialization/mappers, local storage, caching, token refresh hooks. |
| `ui/` | Responsive/adaptive layouts, Material 3, Cupertino, animations, accessibility, foldables, tokens. |
| `platform/` | Permissions, lifecycle, channels, background, foldables, push notifications. |
| `testing/` | Unit/widget/integration/golden testing plus mocking and CI topics. |
| `performance/` | Jank, rebuilds, DevTools, memory, images, isolates, profiling. |
| `build_release/` | Flavors, signing, CI/CD, versioning, stores. |
| `advanced/` | Code generation, FFI, render objects, modular SDKs, web/desktop. |
| `playbooks/` | Procedural debugging/refactoring/migrations. |
| `quality_bar/` | Checklists for definition of done, code/architecture/performance reviews. |
| `templates/` | Canonical templates for skills and checklists. |

## Contribution workflow

1. Read [META.md](./META.md) to understand global conventions.
2. Use the templates:
   - [templates/SKILL_TEMPLATE.md](./templates/SKILL_TEMPLATE.md)
   - [templates/CHECKLIST_TEMPLATE.md](./templates/CHECKLIST_TEMPLATE.md)
3. Keep each skill doc concise (target 80-180 lines; max 220 if needed) and focused on one topic.
4. Update the relevant domain hub `SKILL.md` with links and, if it’s a general entry point, update `SKILL_INDEX.md`.
5. Follow the template’s structure (purpose, when to use/not, core concepts, patterns, example, edge cases, mistakes, testing, related links).

## Portability rules

- Avoid editor-specific steps (no “click X” or “Cursor panel” references).
- Never commit secrets, API keys, or private endpoints.
- Prefer minimal runnable examples: small Flutter/Dart snippets that compile with minor adjustments.
- Use relative links so docs stay portable across environments.

## Testing strategy

- Unit: pure Dart modules, reducers, notifiers, mappers.
- Widget: UI/state wiring, navigation flows, layout/responsiveness.
- Integration: routing (deep links, guards), data flows (token refresh), platform channels, foldable posture changes.

## Common mistakes

- Mixing multiple topics in a single doc (makes retrieval harder).
- Forgoing edge cases and testing guidance.
- Writing UI instructions tied to a specific tool or environment.

## Edge cases to call out

- Platform differences (iOS/Android/web/desktop) can surface divergent behavior.
- Async flows and navigation often expose lifecycle timing issues.
- Foldables/multi-window work introduces posture-dependent layouts.

## License

MIT License ([LICENSE](./LICENSE))

## Security

Follow [SECURITY.md](./SECURITY.md) when reviewing vulnerabilities or dependency risks. Report findings via GitHub Security Advisories or the repository issue tracker (mark as security-related) so maintainers can triage safely.

## Related resources

- Router: [SKILL_INDEX.md](./SKILL_INDEX.md)
- Global conventions: [META.md](./META.md)
