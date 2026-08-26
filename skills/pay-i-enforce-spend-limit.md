---
name: pay-i-enforce-spend-limit
description: Create, inspect, reset and retire a Pay-i spend Limit, and read the per-limit state returned on every proxied GenAI request.
api: Pay-i API
base_url: https://api.pay-i.com
operations:
  - createLimit
  - getLimits
  - getLimit
  - updateLimit
  - updateLimitProperties
  - resetLimit
  - deleteLimit
---

# Enforce a spend limit with Pay-i

Limits are Pay-i's control plane. They cap GenAI spend rather than request rate.

## Auth
Send the application API key in the `xProxy-api-key` header on every call. Organization-level keys
manage org settings only and will not work here. See https://docs.pay-i.com/docs/pay-i-api-keys.

## Steps

1. **Create the limit** — `POST /api/v1/limits` (`createLimit`). A limit carries a `max` and a risk
   threshold. Decide up front whether it is *blocking*: a blocking limit stops the upstream provider
   call, a non-blocking limit only reports.
2. **Attach it to traffic** — put the limit id in the `xProxy-Limit-IDs` header on your proxied
   requests. Multiple limits go in ONE comma-separated header, not repeated headers.
3. **Read the state on every response** — proxied responses carry an `xproxy_result` object with a
   `state` per limit:
   - `ok` — `spend < max * threshold`
   - `exceeded` — `spend >= max * threshold AND spend <= max`. **This is not blocked.** Requests are
     still allowed. Treat it as the signal to downshift to a cheaper model or upsell, not as a stop.
   - A blocking limit that is genuinely over `max` returns **HTTP 424 Failed Dependency** and the
     upstream provider call is never made. Do not retry a 424 as if it were transient — retrying
     will not clear it.
4. **Inspect** — `GET /api/v1/limits` (`getLimits`) is cursor-paginated: pass `cursor`, `limit`,
   `sort_ascending`, and follow the `cursor` field in the response. `GET /api/v1/limits/{limit_id}`
   (`getLimit`) reads one.
5. **Adjust** — `PUT /api/v1/limits/{limit_id}` (`updateLimit`) changes the definition;
   `PUT /api/v1/limits/{limit_id}/properties` (`updateLimitProperties`) changes only the property bag.
6. **Reset** — `POST /api/v1/limits/{limit_id}/reset` (`resetLimit`) clears accumulated spend and
   unblocks traffic. This is the API's undo. **Pay-i publishes no window or restriction on reset**,
   so do not assume one either way.
7. **Retire** — `DELETE /api/v1/limits/{limit_id}` (`deleteLimit`). No restore operation is
   documented; treat deletion as permanent.

## Cautions
- **There is no idempotency key on any Pay-i write operation.** A retried `createLimit` after a
  timeout can create a second limit. Call `getLimits` and reconcile before retrying rather than
  blind-retrying.
- Errors return a stable `code` plus an unstable `message`. Branch on `code` only —
  `limit_not_found`, `create_limit_validation_failed`, `update_limit_validation_failed`,
  `invalid_api_key`. See errors/pay-i-error-codes.yml.
- Block limits are rejected on ingest requests (`blocking_limit_not_allowed`); they apply to
  proxied traffic only.
