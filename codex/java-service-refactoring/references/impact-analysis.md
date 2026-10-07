# Impact analysis

Start from the exact changed method, class, API field, query, or event type. Trace:

1. Entry points: REST controllers, scheduled jobs, message consumers, CLI/administrative entry points, and direct callers.
2. Control and state: validation, authorization, feature flags, transaction boundaries, exceptions, retries, and state transitions.
3. Outbound effects: database reads/writes, cache operations, external clients, emitted events, logs/audit records, and acknowledgements.
4. Delayed paths: asynchronous consumers, retry/DLQ routes, cache invalidation, callbacks, and reconciliation jobs.

For each path, state the behavior that must remain stable and evidence it with callers, tests, configuration, or runtime observations. Examples include the response/error mapping, one-time event processing, rollback semantics, authorization ownership, cache invalidation, and message acknowledgement order.

Compilation proves type-level compatibility only. Add a test, contract check, or targeted runtime observation for behavior that may change without a compiler error. Do not call a path unaffected if its caller or side effect has not been inspected.
