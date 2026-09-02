---
skill: ef-core-patterns
used_by: [backend-engineer, database-engineer]
---

# EF Core Patterns

## Querying
- Use `AsNoTracking()` for read-only queries.
- Project into DTOs with `Select()` instead of loading full entities
  when you only need a subset of fields.
- Use `.Include()`/`.ThenInclude()` deliberately to avoid N+1 lazy-load
  round trips; prefer explicit includes over enabling lazy loading
  globally.

## Migrations
Generate migrations from model changes (`dotnet ef migrations add`),
review the generated SQL before applying, and never hand-edit a
migration that has already been applied to a shared environment.

## Transactions
Wrap multi-step writes that must succeed or fail together in an
explicit transaction (`DbContext.Database.BeginTransaction()` or
`SaveChanges` within a single unit-of-work scope) rather than assuming
implicit atomicity across multiple `SaveChanges()` calls.

## Concurrency
Use a `RowVersion`/concurrency token column for optimistic concurrency
on records that can be edited by multiple users, and handle
`DbUpdateConcurrencyException` explicitly rather than letting it
surface as a raw 500.

## Anti-patterns
- Fetching an entire table into memory to filter/aggregate in C# when
  the database can do it in one query.
- Long-lived `DbContext` instances shared across requests (scope
  per-request in ASP.NET Core, which is the framework default).
