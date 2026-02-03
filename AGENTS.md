<INSTRUCTIONS>
These instructions define a universal "skills" knowledge base for Flutter/Dart development that should work in:
- OpenAI Codex (this repo style)
- Cursor (project rules)
- Claude Code (CLAUDE.md style rules)

## What this repo contains
- Primary knowledge base: `flutter-skill-cloud/` (portable Markdown docs)
- Entry point: `flutter-skill-cloud/SKILL_INDEX.md`
- Style/conventions: `flutter-skill-cloud/META.md`

## How to use (workflow)
1) Route the request:
   - Start at `flutter-skill-cloud/SKILL_INDEX.md` to choose the right domain/topic.
2) Load only what you need:
   - Open the relevant domain hub `flutter-skill-cloud/<domain>/SKILL.md`.
   - Then open the specific topic file(s) linked from that hub.
3) Apply the guidance to the user's codebase:
   - Provide a concrete plan and minimal code changes.
   - Prefer patterns that are testable and keep boundaries clear.
4) Keep responses portable:
   - Avoid editor-specific UI steps and proprietary tooling assumptions.
   - Prefer general commands and concepts.

## Domain router (quick map)
- Flutter UI/responsive/foldables: `flutter-skill-cloud/ui/SKILL.md`
- Dart async/null-safety/isolates: `flutter-skill-cloud/dart/SKILL.md`
- Flutter core (context/lifecycle/layout/keys): `flutter-skill-cloud/flutter_core/SKILL.md`
- State (Riverpod/BLoC + async/error/caching): `flutter-skill-cloud/state/SKILL.md`
- Navigation (go_router + deep links): `flutter-skill-cloud/navigation/SKILL.md`
- Architecture (clean boundaries/DI/repos/errors): `flutter-skill-cloud/architecture/SKILL.md`
- Data (networking/serialization/storage): `flutter-skill-cloud/data/SKILL.md`
- Platform (permissions/notifications/channels/lifecycle): `flutter-skill-cloud/platform/SKILL.md`
- Testing (unit/widget/integration/goldens/CI): `flutter-skill-cloud/testing/SKILL.md`
- Performance (jank/rebuilds/memory/images/devtools): `flutter-skill-cloud/performance/SKILL.md`
- Build & release (flavors/signing/stores/versioning): `flutter-skill-cloud/build_release/SKILL.md`
- Advanced (codegen/FFI/render objects/modular SDKs): `flutter-skill-cloud/advanced/SKILL.md`

## Content rules
- No secrets: never include API keys, internal URLs, customer identifiers, or credentials.
- Prefer small, runnable-in-spirit snippets; use `// ...` to omit irrelevant code.
- Model errors as data when it improves UX and testing; avoid blanket try/catch patterns.
- When adding new docs, follow naming/style rules in `flutter-skill-cloud/META.md`.
</INSTRUCTIONS>

