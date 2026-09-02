---
skill: sql-server-and-tsql
used_by: [database-engineer, architect]
---

# SQL Server & T-SQL

## Schema design
- Every table has an explicit primary key; prefer surrogate keys
  (identity/sequence) unless a natural key is stable and simple.
- Enforce integrity with foreign keys and check constraints at the
  database level — don't rely on application code alone.
- Normalize by default (3NF); denormalize deliberately, only where a
  measured performance need justifies it, and document why.

## Indexing
- Index columns used in `WHERE`, `JOIN`, and `ORDER BY` on
  frequently-run queries.
- Watch for missing indexes on foreign keys — SQL Server doesn't add
  these automatically.
- Avoid over-indexing tables with heavy write volume; every index has
  an insert/update cost.

## Query patterns
- Prefer set-based T-SQL over row-by-row cursors.
- Use `EXISTS` over `COUNT(*) > 0` for existence checks.
- Watch execution plans for table scans on large tables and for
  implicit conversions (mismatched column/parameter types) that
  silently disable index usage.
- Guard against N+1 query patterns from the application layer — one
  query with a proper join/include beats N+1 round trips.

## Transactions & concurrency
Choose isolation level deliberately (READ COMMITTED is the SQL Server
default and fine for most OLTP work); use `ROWVERSION`/optimistic
concurrency for typical web-app update conflicts rather than heavy
locking.

## Migrations
Every schema change ships as a migration script, forward and (where
feasible) backward. Never edit a schema directly against a shared
environment without a migration recorded.

## Stored procedures
Justified for: bulk operations, complex multi-step reporting queries,
or when centralizing logic across multiple app clients. Not justified
as a default location for ordinary CRUD logic that EF Core handles
cleanly.
