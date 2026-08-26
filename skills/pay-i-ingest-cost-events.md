---
name: pay-i-ingest-cost-events
description: Submit GenAI cost and usage events to Pay-i for providers it does not proxy, including bulk and upsert paths and Microsoft Copilot transcripts and licensing.
api: Pay-i API
base_url: https://api.pay-i.com
operations:
  - requests.Ingest
  - requests.BulkIngest
  - requests.BulkUpsert
  - requests.CopilotTranscriptIngest
  - requests.CopilotLicensingIngest
---

# Ingest cost events into Pay-i

Use ingest when the traffic did not go through the Pay-i proxy — a provider Pay-i does not front,
an offline batch, or a platform like Microsoft Copilot that reports its own usage.

## Operations
- `POST /api/v1/ingest` (`requests.Ingest`) — one event.
- `POST /api/v1/ingest/bulk` (`requests.BulkIngest`) — many events.
- `POST /api/v1/ingest/bulk-upsert` (`requests.BulkUpsert`) — many events with upsert semantics
  keyed on caller-supplied identifiers.
- `POST /api/v1/ingest/copilot/transcripts` (`requests.CopilotTranscriptIngest`)
- `POST /api/v1/ingest/copilot/licensing` (`requests.CopilotLicensingIngest`)

Docs: https://docs.pay-i.com/docs/manual-event-submission, https://docs.pay-i.com/docs/rest-ingest

## Rules the API enforces
- `event_timestamp` **cannot be more than 5 minutes in the future** — violating it returns
  `invalid_ingest_event_timestamp`. Clamp to now if your clock may drift.
- **Blocking limits are rejected on ingest** — `blocking_limit_not_allowed`. Attach non-blocking
  limits only. Ingest is a reporting path; it cannot stop traffic that already happened.
- Attribution uses the same header vocabulary as the proxy: `xProxy-User-ID`,
  `xProxy-Account-Name`, `xProxy-UseCase-Name`, `xProxy-Request-Properties`.

## Retry safety — read this before writing a retry loop
Pay-i publishes **no idempotency key** on any ingest operation, and there is **no delete, void or
reverse operation for an ingested event**. A double-submitted batch permanently double-counts spend
in a product whose entire purpose is accurate cost attribution.

- Prefer `bulk-upsert` over `bulk` for anything that might be retried, and supply your own stable
  identifiers so the upsert can deduplicate.
- On a timeout or a 5xx with no response body, do **not** blind-retry `requests.Ingest` or
  `requests.BulkIngest`. Reconcile first with `getRequestResult` / `getRequestResultProvider`.
- Treat `unexpected_error` and `request_processing_error` differently: the second is a validation
  failure and retrying the identical payload will fail identically.
