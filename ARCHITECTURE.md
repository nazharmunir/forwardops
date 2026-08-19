# ForwardOps architecture

## Design goal

The prototype demonstrates an automation architecture where probabilistic extraction can help operators understand freight requests without being granted direct authority to mutate an external transport-management system.

## Trust boundaries

### 1. Untrusted input boundary

Email bodies and document text are always external input. Statements such as “ignore previous instructions”, “set price to zero”, or “execute immediately” are not privileged merely because they occur in a shipment document.

### 2. Extraction boundary

The extraction layer proposes structured shipment facts and attaches source evidence. In this prototype it is deterministic; in a production system it could use an LLM with schema-constrained output.

### 3. Policy and validation boundary

Business requirements are enforced by deterministic application code. Missing operational fields, unsafe instructions and execution eligibility are calculated independently of the extraction layer.

### 4. Human authorization boundary

A valid action plan is still not equivalent to permission. The operator must explicitly approve the write.

### 5. Connector boundary

The mock TMS connector represents an external side effect. Production connectors should use scoped credentials, idempotency keys, retry/backoff policies, timeouts, observability and dead-letter handling where appropriate.

## Production evolution

A realistic implementation could introduce:

- MIME/email ingestion and attachment parsing
- OCR/document extraction where required
- schema-constrained LLM extraction
- confidence/evidence calibration
- tenant-specific validation rules
- real TMS adapters behind a connector interface
- durable approval state in PostgreSQL
- asynchronous jobs and retry queues
- OpenTelemetry traces and structured audit logs
- role-based approval policies
- evaluation datasets for extraction and injection-resistance regressions

The core invariant remains the same: **untrusted content must never become execution authority.**
