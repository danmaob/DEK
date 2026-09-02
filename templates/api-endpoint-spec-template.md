# API Endpoint Specification

## Endpoint
`<METHOD> <path>`

## Purpose
<What this endpoint does, in one or two sentences>

## Authentication
<Required? What scheme/role?>

## Request
**Path/query parameters:**
<name>: <type> — <description>

**Body:**
```json
{
  "field": "type — description"
}
```

## Response

### Success (`<status code>`)
```json
{
  "field": "type — description"
}
```

### Error responses
| Status | Condition | Body shape |
|---|---|---|
| 400/422 | Validation failure | error code + field-level details |
| 401/403 | Auth failure | error code + message |
| 404 | Resource not found | error code + message |
| 409 | Conflict | error code + message |

## Notes
<Pagination, rate limits, idempotency, or other relevant behavior>
