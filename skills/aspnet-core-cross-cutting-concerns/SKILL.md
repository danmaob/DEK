---
skill: aspnet-core-cross-cutting-concerns
used_by: [backend-engineer]
---

# ASP.NET Core Cross-Cutting Concerns

## Dependency injection
Register services with the narrowest lifetime that is correct:
`Scoped` for anything touching `DbContext` or per-request state,
`Singleton` for stateless/thread-safe services, `Transient` sparingly.
Constructor-inject dependencies; avoid `IServiceProvider` as a manual
service locator.

## Configuration & options
Bind configuration sections to strongly-typed `Options` classes
(`IOptions<T>`/`IOptionsSnapshot<T>`) instead of reading raw
`IConfiguration` strings scattered through the codebase. Never commit
real secrets to `appsettings.json` — use user secrets locally and the
platform's secret manager in deployed environments.

## Exception handling
Use a global exception-handling middleware to translate unhandled
exceptions into a consistent error response shape (see
`api-design`); never leak stack traces or internal exception messages
to clients in non-development environments.

## Structured logging
Log structured events (not string-concatenated messages) with
correlation/trace IDs so a request can be followed across services.
Never log secrets, tokens, passwords, or full request bodies containing
personal data.
