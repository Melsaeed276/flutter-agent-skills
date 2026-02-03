# Skill: Repository Security Practices

## Purpose
This document captures how to review and report security-related matters for the Universal Flutter Skills Cloud repository.

## When to use
- You discover a vulnerability (leak, secret, unsafe dependency, insecure logic).
- You need to report a dependency or configuration risk.

## When NOT to use
- Do not use this to discuss general bugs; open a regular issue instead.

## Core concepts
- **No secrets**: do not commit API keys, credentials, or private endpoints.
- **Evidence**: capture reproduction steps and logs (without sharing secrets).
- **Responsibility**: rely on repository maintainers to triage and mitigate issues.

## Recommended patterns
- Review dependency updates for known CVEs before merging.
- Use scanning tools (e.g., `pub outdated`, `dart pub upgrade`, `git-secrets`) as part of CI if you add them.
- Keep cryptographic operations up-to-date and avoid home-grown crypto.

## Minimal example

```text
1) Run `dart pub outdated --mode=null-safety` to check dependencies.
2) Review `pubspec.lock` for transitive packages with CVEs.
3) If you find an issue, open a GitHub Security Advisory or email the maintainer specified in package metadata.
```

## Edge cases
- New vulnerabilities often explain which versions to pin; follow the CVE guidance precisely.
- Security reports may contain sensitive reproduction data; redact secrets before sharing.

## Common mistakes
- Including credentials when sharing logs; remove API keys or tokens.
- Assuming that a private repository eliminates the need for security review.

## Testing strategy
- Automate dependency scanning (e.g., `dart pub outdated`, `pub audit`).
- Add linting/hardening steps in CI if you introduce native plugins or platform channels.

## Related skills
- [META conventions](./META.md)
- [Quality bar checklists](./quality_bar/definition_of_done.md)
