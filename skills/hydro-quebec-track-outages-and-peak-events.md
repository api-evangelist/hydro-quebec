---
name: Track Hydro-Québec outages and winter peak events
description: Poll the ongoing-outage, planned-interruption and winter peak-demand datasets, and understand why polling is the only option — there is no webhook or event stream.
api: openapi/hydro-quebec-open-data-explore-api-v2-1-openapi.json
base_url: https://donnees.hydroquebec.com/api/explore/v2.1
operations: [getDataset, getRecords, getRecordsFacets, exportRecords]
generated: '2026-07-27'
method: generated
---

# Track Hydro-Québec outages and winter peak events

These are the event-shaped datasets in the catalog. **Hydro-Québec publishes no webhooks, no
streaming endpoint and no AsyncAPI** — so "tracking" means polling the same read endpoints on a
schedule and diffing.

## The datasets

| dataset_id | What it is |
|---|---|
| `pannes-interruptions` | Ongoing outages and planned service interruptions |
| `evenements-pointe` | Winter peak demand events (473 records) |
| `evenements-de-pointe-offres-disponibles` | Winter peak events — available offers (75 records) |
| `consommation-clients-evenements-pointe` | Consumption of customers in a local demand response programme (64,605 records) |

## Steps

1. **Read the schema before the first poll** — call `getDataset` on
   `/catalog/datasets/{dataset_id}`. Verified fields on `evenements-pointe`: `offre` (text),
   `datedebut` (datetime), `datefin` (datetime), `plagehoraire` (text), `duree` (text),
   `secteurclient` (text).

2. **Poll `getRecords`** on `/catalog/datasets/{dataset_id}/records`. For the outage dataset,
   fetch the current set each cycle and diff against your previous snapshot to derive
   opened/updated/closed events — the API exposes no change feed and no delta parameter.

3. **Filter to the active window** with a `where` clause over the datetime fields using the
   ODSQL date functions (`now()`, `year()`, `month()`, `day()`, `hour()`). Set `timezone` so
   comparisons land in Eastern time rather than UTC — Québec peak events are defined in local
   morning and evening blocks.

4. **Enumerate the categories once** — call `getRecordsFacets` with `facet=offre`,
   `facet=secteurclient` or `facet=plagehoraire` on `evenements-pointe` to learn the real
   category values instead of hard-coding labels from a blog post.

5. **Backfill history with an export** — `consommation-clients-evenements-pointe` is 64,605
   records. Use `exportRecords` (Parquet) for the historical load, then poll only the small
   current datasets going forward.

6. **Check `metas.default.modified`** on each poll via `getDataset`. If it has not advanced,
   nothing has changed and you can skip the record fetch entirely — this is the cheapest possible
   change detector on an API with no `ETag` and no `Last-Modified`.

## Rules

- **Poll politely.** Read `X-RateLimit-Remaining` and `X-RateLimit-Reset` on every response. The
  reset value is a `YYYY-MM-DD HH:MM:SS+00:00` timestamp resetting at midnight UTC, not epoch
  seconds. On `429` the body carries `errorcode` 10002 with `call_limit` and `reset_time` — back
  off to `reset_time`.
- **`pannes-interruptions` reported `records_count` 0 at the time of capture (2026-07-27).** An
  empty result is a legitimate state (no outages, or the dataset is refreshed on event), not an
  error. Do not treat zero rows as a failure.
- Responses set `Cache-Control: no-store` and return no validators, so every poll is a full
  fetch. Keep the polling interval honest — minutes, not seconds.
- All operations are `GET` and idempotent; a dropped poll can simply be repeated.
- `404 NotFoundResource` means the `dataset_id` is wrong — re-resolve it from `getDatasets`.
- This is grid and programme data, **not** customer data. There is no per-customer outage status,
  no premise or service-point entity, and no way to ask "is my address out" through this API.
- CC BY-NC 4.0: attribute, flag modifications, link the licence, non-commercial only. Do not
  present derived outage counts as an official Hydro-Québec figure.
