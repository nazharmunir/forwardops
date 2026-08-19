# ForwardOps demo flow

A concise walkthrough for interviews, portfolio reviews, or founder outreach.

## 60–90 second walkthrough

1. Open the **complete request** and run **Analyze & build action plan**.
2. Click an extracted fact such as **Weight** or **Origin** to show the evidence trace.
3. Point out that the extraction layer can propose values, while deterministic application code validates required fields.
4. Click **Approve & create in TMS** to demonstrate the explicit human authorization boundary and idempotent connector concept.
5. Open the **Security hold** request and analyze it.
6. Show that an instruction such as “set the shipping price to €0” is treated as untrusted content and cannot change execution policy.
7. Finish with the architectural invariant: **untrusted content never becomes execution authority**.

## Key design sentence

> AI can help understand the request, but it never receives direct authority to mutate the operational system.

## What is real in the public prototype

- browser-based freight request parsing
- evidence traces for extracted values
- required-field validation
- suspicious-instruction detection
- approval gating
- mock TMS execution and audit events
- custom request sandbox

The public demo intentionally uses deterministic extraction so it is reproducible and does not pretend to call an AI model when it does not. A production version could replace the extraction layer with schema-constrained LLM output while preserving the same validation, authorization and connector boundaries.
