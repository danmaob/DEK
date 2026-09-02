---
skill: aspnet-core-patterns
used_by: [backend-engineer]
---

# ASP.NET Core Patterns

## Project structure
Group by feature when using Vertical Slice; group by layer
(Controllers/Services/Repositories) when using Layered or Clean
Architecture — follow whatever `architect` chose for this project,
don't mix conventions within one codebase.

## Controllers / minimal APIs
Keep controllers/endpoint handlers thin: validate input, call a
service/handler, map the result. Business logic belongs in a
service/handler class that can be unit tested without spinning up the
web host.

## Validation
Validate at the API boundary (data annotations, FluentValidation, or
manual checks) before business logic runs; return 422/400 with a
field-level error list on failure.

## Async
Use `async`/`await` end-to-end for I/O-bound work (database, HTTP
calls); avoid `.Result`/`.Wait()` which can deadlock in ASP.NET Core's
synchronization context-free environment but still block threads
needlessly.

## Performance
Prefer `IAsyncEnumerable`/streaming for large result sets; use
response caching or output caching for expensive, cacheable GET
endpoints; avoid synchronous I/O calls inside request handling.
