# Skill: Dio HTTP Client

## Purpose
Covers the full lifecycle of HTTP networking in Flutter using Dio: setup, environment config, authentication (Bearer / API-key / refresh-token), logging, error handling, and response caching — all through the interceptor pipeline.

## When to use
- Any Flutter feature that makes REST calls (GET / POST / PUT / PATCH / DELETE).
- You need per-environment base URLs (dev / staging / prod).
- Auth tokens must be attached or refreshed automatically.
- You want centralised logging or error mapping without repeating code in every call site.

## When NOT to use
- Pure offline or local-only data (use Hive / Isar directly).
- WebSocket or SSE streams (use `dart:io` WebSocket or a dedicated package).
- Already wrapped behind a generated client (e.g. `dio_generator` / OpenAPI codegen) — those handle options internally.

## Core concepts

**Singleton Dio instance** — create one `Dio` per app (or one per auth-scope). Reuse it everywhere so `BaseOptions` and interceptors apply globally.

**Interceptor pipeline** — every request passes through `onRequest → server → onResponse / onError`. Stack interceptors in order: Auth first, Logger second, ErrorMapper last.

**BaseOptions vs Options** — `BaseOptions` sets app-wide defaults (baseUrl, timeouts, headers). Per-call `Options` override only what differs. They are merged at request time.

**DioExceptionType enum** — all Dio errors surface as `DioException`. The `.type` field tells you *why* it failed (timeout, bad response, cancelled, etc.).

## Recommended patterns

### 1. Environment-aware singleton

```dart
// env.dart
enum Env { dev, staging, prod }

const Env currentEnv = Env.dev; // swap at build via flavors/--dart-define

String get baseUrl => switch (currentEnv) {
  Env.dev     => 'http://10.0.2.2:3000/api',   // Android emulator
  Env.staging => 'https://staging.example.com/api',
  Env.prod    => 'https://api.example.com/api',
};
```

> iOS simulator localhost = `127.0.0.1`; Android emulator = `10.0.2.2`.

### 2. Interceptor order

```
dio.interceptors.add(AuthInterceptor());   // 1 – attach / refresh token
dio.interceptors.add(LogInterceptor());    // 2 – log after auth header is set
dio.interceptors.add(ErrorInterceptor());  // 3 – map errors last
```

### 3. Auth interceptor — Bearer + refresh

```dart
class AuthInterceptor extends Interceptor {
  final TokenStorage storage;          // flutter_secure_storage wrapper
  final Dio _refreshDio;               // separate Dio — avoids infinite loop
  Completer<String?>? _refreshCompleter;

  @override
  Future<void> onRequest(RequestOptions options, RequestInterceptorHandler handler) async {
    final token = await storage.readAccessToken();
    if (token != null) options.headers['Authorization'] = 'Bearer $token';
    handler.next(options);
  }

  @override
  Future<void> onError(DioException err, ErrorInterceptorHandler handler) async {
    if (err.response?.statusCode != 401) return handler.next(err);

    // Only one refresh in flight at a time (Completer pattern).
    if (_refreshCompleter == null) {
      _refreshCompleter = Completer();
      try {
        final newToken = await _doRefresh();
        await storage.writeAccessToken(newToken);
        _refreshCompleter!.complete(newToken);
      } catch (e) {
        _refreshCompleter!.completeError(e);
      } finally {
        _refreshCompleter = null;
      }
    }

    final token = await _refreshCompleter!.future;
    // Retry original request with fresh token.
    final opts = err.requestOptions.copyWith(
      headers: {
        ...err.requestOptions.headers,
        'Authorization': 'Bearer $token',
      },
    );
    handler.resolve(await dio.fetch(opts));
  }

  Future<String> _doRefresh() async {
    final refresh = await storage.readRefreshToken();
    final res = await _refreshDio.post('/auth/refresh', data: {'refreshToken': refresh});
    return res.data['accessToken'];
  }
}
```

### 4. API-key auth (simpler — no refresh needed)

```dart
@override
Future<void> onRequest(RequestOptions options, RequestInterceptorHandler handler) async {
  options.headers['X-Api-Key'] = const String.fromEnvironment('API_KEY');
  handler.next(options);
}
```

### 5. Error mapping interceptor

```dart
class ErrorInterceptor extends Interceptor {
  @override
  Future<void> onError(DioException err, ErrorInterceptorHandler handler) async {
    final AppException mapped = switch (err.type) {
      DioExceptionType.connectionTimeout,
      DioExceptionType.sendTimeout,
      DioExceptionType.receiveTimeout => TimeoutAppException(),
      DioExceptionType.connectionError => NoInternetAppException(),
      DioExceptionType.badResponse     => ServerAppException(err.response?.statusCode ?? 0),
      DioExceptionType.requestCancelled => CancelledAppException(),
      _                                => UnknownAppException(err.message),
    };
    handler.reject(mapped.toDioException(err.requestOptions));
  }
}
```

## Minimal example

```dart
import 'package:dio/dio.dart';

// Single entry-point — inject this via get_it / Riverpod / etc.
final Dio dio = Dio(
  BaseOptions(
    baseUrl: baseUrl,                          // from env.dart
    connectTimeout: const Duration(seconds: 10),
    receiveTimeout: const Duration(seconds: 30),
    headers: {'Accept': 'application/json'},
  ),
)..interceptors.addAll([
  AuthInterceptor(storage: TokenStorage()),
  LogInterceptor(logPrint: (o) => debugPrint(o.toString())),
]);

// Usage
Future<List<User>> fetchUsers() async {
  final res = await dio.get('/users');
  return (res.data as List).map(User.fromJson).toList();
}
```

## Edge cases

- **Multiple 401s in parallel** — without the Completer pattern every failed request fires its own refresh. The Completer guarantees exactly one refresh call; others await the same future.
- **Refresh token itself expired** — if `_doRefresh` throws, reject the original request and route the user to login. Never retry a refresh.
- **File upload retry after 401** — `MultipartFile.fromFile` is a stream; it cannot be re-read. Re-create the `FormData` from the original file path before retrying.
- **localhost on emulator** — `localhost` does NOT resolve to the host machine. Use `10.0.2.2` (Android) or `127.0.0.1` (iOS simulator).
- **SSL in dev** — only disable certificate validation in debug builds; never ship it.

## Common mistakes

1. **Creating a new `Dio()` per request** — interceptors and base config are lost. Always reuse the singleton.
2. **Using `SharedPreferences` for tokens** — stores plain text. Use `flutter_secure_storage` (iOS Keychain / Android Keystore).
3. **Using the same `Dio` instance for the refresh call** — causes the auth interceptor to intercept the refresh request itself → infinite 401 loop.
4. **Ignoring `DioExceptionType`** — catching only `statusCode` misses timeouts, cancellations and connection errors entirely.
5. **Logging sensitive data in production** — wrap `LogInterceptor` in a `kDebugMode` guard.
6. **Not setting `sendTimeout`** — large uploads can hang silently without it.

## Testing strategy

**Unit tests** — mock `Dio` using `diohttp` or a custom `HttpClientAdapter`. Verify interceptor logic (token attachment, error mapping) in isolation.

**Integration tests** — point `baseUrl` at a local mock server (e.g. `mockServer` or `json_server`). Run full request → interceptor → parse cycles.

**Interceptor-specific tests** — create a `Dio` instance in test, add only the interceptor under test, and use a `MockAdapter` to return controlled status codes (401, 500, timeout). Assert the transformed output or the retry behaviour.

## Related skills
- `state_management/riverpod.md` — injecting the Dio singleton via providers.
- `local_storage/secure_storage.md` — token persistence patterns.
- `architecture/clean_architecture.md` — repository layer wrapping Dio calls.
- `testing/widget_testing.md` — mocking network in widget tests.
