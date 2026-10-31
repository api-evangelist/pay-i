# Pay-i

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Pay-i is a GenAI cost, capacity and ROI optimization platform founded by Microsoft veterans. It instruments generative-AI applications so enterprises can prove the business value of their AI spend. Pay-i exposes a REST API at api.pay-i.com built around three surfaces: a metering proxy that fronts OpenAI, Azure OpenAI, Anthropic, Azure Anthropic, AWS Bedrock and Google Vertex and records cost, latency and failure metadata for every inference request; an ingest API for submitting events from providers Pay-i does not proxy; and a management API covering Limits (spend budgets with risk thresholds and blocking states), Use Cases and their versions and instances, KPIs and value policies, Categories and Resources for model and price catalogs, and Reports. Instrumentation is driven by a family of xProxy-* request headers and first-party Python and TypeScript SDKs, plus an n8n community node and a Databricks integration.

**Areas:** Company · Artificial Intelligence · FinOps · Observability · Cost Management · Generative AI · LLM · Analytics · Governance · Metering

## Pay-i on APIs.io

Everything profiled for Pay-i is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/pay-i/](https://apis.io/providers/pay-i/)** — or go straight to one of the APIs or properties below.

### APIs (14)

- [Pay-i Anthropic Requests API](https://apis.io/apis/pay-i/pay-i-anthropic-requests-api/) — Anthropic Requests
- [Pay-i AWS Bedrock Requests API](https://apis.io/apis/pay-i/pay-i-aws-bedrock-requests-api/) — AWS Bedrock Requests
- [Pay-i Azure Anthropic Requests API](https://apis.io/apis/pay-i/pay-i-azure-anthropic-requests-api/) — Azure Anthropic Requests
- [Pay-i Azure OpenAI Requests API](https://apis.io/apis/pay-i/pay-i-azure-openai-requests-api/) — Azure OpenAI Requests
- [Pay-i Categories API](https://apis.io/apis/pay-i/pay-i-categories-api/) — System and Custom Categories
- [Pay-i Google Vertex Requests API](https://apis.io/apis/pay-i/pay-i-google-vertex-requests-api/) — Google Vertex Requests
- [Pay-i Ingest Events API](https://apis.io/apis/pay-i/pay-i-ingest-events-api/) — Ingest Requests
- [Pay-i KP Is API](https://apis.io/apis/pay-i/pay-i-kpis-api/) — KPIs
- [Pay-i Limits API](https://apis.io/apis/pay-i/pay-i-limits-api/) — Limits
- [Pay-i OpenAI Requests API](https://apis.io/apis/pay-i/pay-i-openai-requests-api/) — OpenAI Requests
- [Pay-i Reports API](https://apis.io/apis/pay-i/pay-i-reports-api/) — Public API for retrieving reports.
- [Pay-i Requests API](https://apis.io/apis/pay-i/pay-i-requests-api/) — Requests
- [Pay-i Resources API](https://apis.io/apis/pay-i/pay-i-resources-api/) — Resources
- [Pay-i Use Cases API](https://apis.io/apis/pay-i/pay-i-use-cases-api/) — Use Cases

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [pay-i-docs](https://apis.io/servers/pay-i/pay-i-docs/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Pay I Openapi Overlay](https://apis.io/overlays/pay-i/pay-i-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Pay I Authentication](https://apis.io/security/pay-i/pay-i-authentication/)
- [Pay I Domain Security](https://apis.io/security/pay-i/pay-i-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Pay I Plans Pricing](https://apis.io/plans/pay-i/pay-i-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Pay I Rate Limits](https://apis.io/rate-limits/pay-i/pay-i-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.pay-i.com/)
- [Documentation](https://docs.pay-i.com/docs/getting-started)
- [Getting started](https://docs.pay-i.com/docs/getting-started)
- [API reference](https://docs.pay-i.com/reference/getlimits)
- [Sign up](https://developer.pay-i.com/login)
- [Blog](https://www.pay-i.com/resources)
- [Terms of service](https://www.pay-i.com/tos)
- [Privacy policy](https://www.pay-i.com/privacy)
- [GitHub](https://github.com/Pay-i)

## API Evangelist rating

**Kin Score 38.9** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 48.3 |
| Contract governance | 4.5 |
| Operational transparency | 2.6 |
| Developer ergonomics | 47.0 |
| Access clarity | 34.2 |

**Agent readiness 29.3** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 22.7** — AI & Biometrics

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/pay-i/](https://apis.io/providers/pay-i/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Pay-i: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/pay-i/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
