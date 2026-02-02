# Riverpod Providers

## Patterns

- Use providers for wiring dependencies (clients, repositories).
- Keep providers small; compose rather than building mega-providers.

## Pitfalls

- Reading providers in places where lifecycle is unclear.

## Example (dependency wiring)

```dart
final apiClientProvider = Provider<ApiClient>((ref) => ApiClient());
final userRepoProvider = Provider<UserRepo>((ref) => UserRepo(ref.read(apiClientProvider)));
```

