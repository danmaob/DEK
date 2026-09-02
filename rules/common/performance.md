# Rule: Performance

- Database queries avoid N+1 patterns; a change that introduces one
  is a blocking review finding once identified.
- I/O-bound backend code is asynchronous end-to-end.
- Expensive, cacheable reads use caching deliberately, not
  incidentally; cache invalidation is designed at the same time as
  the cache, not left as a follow-up.
- Performance-sensitive changes are verified against realistic data
  volumes, not just the tiny dataset used during development.
