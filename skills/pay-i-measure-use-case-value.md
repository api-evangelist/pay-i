---
name: pay-i-measure-use-case-value
description: Define a Pay-i Use Case, attach KPI definitions, score instances, and read back the money and time value of a GenAI use case.
api: Pay-i API
base_url: https://api.pay-i.com
operations:
  - createUseCase
  - getUseCases
  - getUseCase
  - updateUseCase
  - incrementUseCaseVersion
  - createUseCaseLimitConfig
  - newUseCaseInstance
  - getUseCaseInstance
  - updateUseCaseInstanceProperties
  - createUseCaseKpiDefinition
  - getKpi
  - updateUseCaseKpiDefinition
  - updateUseCaseInstanceKpi
  - getUseCaseInstanceKpis
  - getUseCaseInstanceValue
---

# Measure the business value of a GenAI use case

This is the flow behind Pay-i's ROI claim: a Use Case is the unit of business work, an instance is
one run of it, and KPIs turn runs into money and time saved.

## 1. Define the use case
- `POST /api/v1/use_cases/definitions` (`createUseCase`)
- `GET /api/v1/use_cases/definitions` (`getUseCases`) — cursor-paginated via `cursor` / `limit` /
  `sort_ascending`
- `PUT /api/v1/use_cases/definitions/{use_case_name}` (`updateUseCase`)

Optionally attach a default limit configuration so every instance inherits spend control:
`POST /api/v1/use_cases/definitions/{use_case_name}/limit_config` (`createUseCaseLimitConfig`).
See https://docs.pay-i.com/docs/use-case-automatic-limits.

## 2. Version it
`POST /api/v1/use_cases/definitions/{use_case_name}/increment_version`
(`incrementUseCaseVersion`). Pin traffic to a version with the `xProxy-UseCase-Version` header so a
prompt or model change does not silently pollute the previous version's measurements.
**There is no decrement or rollback operation** — increments are one-way.

## 3. Define KPIs
- `POST /api/v1/use_cases/definitions/{use_case_name}/kpis` (`createUseCaseKpiDefinition`)
- `GET  /api/v1/use_cases/definitions/{use_case_name}/kpis` (`getKpi`)
- `PUT  /api/v1/use_cases/definitions/{use_case_name}/kpis/{kpi_name}` (`updateUseCaseKpiDefinition`)

## 4. Run and score instances
- `POST /api/v1/use_cases/instances/{use_case_name}` (`newUseCaseInstance`) — start a run. Carry the
  returned id in `xProxy-UseCase-ID` on the proxied GenAI calls that belong to it, and use
  `xProxy-UseCase-Step` to mark position in a multi-step flow.
- `PUT /api/v1/use_cases/instances/{use_case_name}/{use_case_id}/kpis/{kpi_name}`
  (`updateUseCaseInstanceKpi`) — record the outcome.
- `GET .../kpis` (`getUseCaseInstanceKpis`) — all KPI scores for the instance.
- `GET .../value` (`getUseCaseInstanceValue`) — the money and/or time value of the instance. This
  is the payoff call, and the number an ROI dashboard is built on.

## Cautions
- Instance and KPI deletes (`deleteUseCaseInstance`, `deleteUseCaseKpiDefinition`,
  `deleteUseCase`) have **no documented restore path and no stated window**. Deleting a use case
  definition is the widest-blast-radius operation in this flow.
- No idempotency key exists on `newUseCaseInstance`; a retried create can produce a duplicate
  instance and split one run's measurements across two records. Reconcile with `getUseCaseInstance`
  rather than retrying blind.
- Value and KPI reads reflect only what was attributed at request time. If the `xProxy-UseCase-*`
  headers were missing on the proxied calls, the instance will score empty and there is no
  backfill operation for the attribution itself — only `updateRequestProperties` for property bags.
