---
name: pay-i-instrument-genai-requests
description: Route a GenAI provider call through the Pay-i metering proxy and attribute its cost to a user, account and use case using the xProxy-* headers.
api: Pay-i API
base_url: https://api.pay-i.com
operations:
  - requests.OpenAI.ChatCompletionsAPIV1
  - requests.OpenAI.ResponsesAPIV1
  - requests.OpenAI.EmbeddingsAPIV1
  - requests.OpenAI.ImagesGenerationsAPIV1
  - getRequestResult
  - getRequestResultProvider
  - updateRequestProperties
---

# Instrument GenAI requests through the Pay-i proxy

Pay-i fronts the major providers and records cost, latency and failure metadata per request.
Swap the provider base URL for the matching Pay-i proxy path and keep the provider's own request
body unchanged.

## Proxy paths
- OpenAI — `/api/v1/proxy/openai/v1/chat/completions`, `/v1/responses`, `/v1/embeddings`,
  `/v1/images/generations`
- Azure OpenAI — `/api/v1/proxy/azure.openai/openai/deployments/{deploymentName}/chat/completions`
  (also `/embeddings`, `/images/generations`) and `/api/v1/proxy/azure.openai/openai/v1/responses`
- Anthropic — `/api/v1/proxy/anthropic/v1/messages`
- Azure Anthropic — `/api/v1/proxy/azure.anthropic/v1/messages`
- AWS Bedrock — `/api/v1/proxy/aws.bedrock/model/{modelId}/converse` (also `converse-stream`,
  `invoke`, `invoke-with-response-stream`)
- Google Vertex — `/api/v1/proxy/google.vertex/{version}/projects/{project}/locations/{location}/publishers/{publisher}/models/{modelId}:generateContent`
  (also `:streamGenerateContent`, `:rawPredict`, `:streamRawPredict`)

## Attribution headers
All attribution is in headers, so the provider payload stays untouched. Multi-value headers are a
single comma-separated header.

| Header | Use |
|---|---|
| `xProxy-api-key` | Pay-i application key (required) |
| `xProxy-Limit-IDs` | Which limits this request is charged against |
| `xProxy-User-ID` | Free-form user identifier |
| `xProxy-Account-Name` | Account attribution |
| `xProxy-UseCase-Name` / `-ID` / `-Version` / `-Step` | Use case attribution and step within a flow |
| `xProxy-UseCase-Properties` / `xProxy-Request-Properties` | Property bags |
| `xProxy-Resource-Scope` | Which model/price catalog to price against |
| `xProxy-PriceAs-Category` / `-Resource` | Override how the request is priced |
| `xProxy-Provider-BaseUri` | Upstream provider base URI |
| `xProxy-Logging-Disable` | `True` suppresses request/response logging while still accounting cost, error, latency and metadata — use for sensitive payloads |

Full reference: https://docs.pay-i.com/docs/list-of-all-supported-headers

## Reading results back
- `GET /api/v1/requests/{request_id}/result` (`getRequestResult`) — by Pay-i request id.
- `GET /api/v1/requests/provider/{category}/{provider_response_id}/result`
  (`getRequestResultProvider`) — by the **upstream provider's** response id. Use this when you only
  kept the OpenAI/Anthropic id.
- `PUT /api/v1/requests/{request_id}/properties` (`updateRequestProperties`) — enrich after the fact.

## Cautions
- Check `xproxy_result` on every response before assuming the call succeeded end to end.
- **HTTP 424** means a blocking limit stopped the call and the provider never saw it. It is not a
  transient failure and must not be retried on a backoff.
- Prefer the first-party SDKs, which wrap this: `pip install payi` (0.1.0a183) exposes
  `payi_instrument()`, `@track` and `track_context()`. The TypeScript client (`npm install payi`)
  is at 0.0.2 and last published 2026-01-29 — verify coverage before depending on it.
