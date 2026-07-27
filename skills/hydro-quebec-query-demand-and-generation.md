---
name: Query Québec electricity demand and generation
description: Pull Hydro-Québec's demand, generation-mix and import/export series with ODSQL, including time-bucketed aggregates, without paging more than you need.
api: openapi/hydro-quebec-open-data-explore-api-v2-1-openapi.json
base_url: https://donnees.hydroquebec.com/api/explore/v2.1
operations: [getDataset, getRecords, getRecord, getRecordsFacets]
generated: '2026-07-27'
method: generated
---

# Query Québec electricity demand and generation

This is the marquee flow: the Québec grid's load and supply, as time series.

## The datasets

| dataset_id | What it is | Records |
|---|---|---|
| `historique-demande-electricite-quebec` | History of electricity demand in Québec | 52,608 |
| `demande-electricite-quebec` | Current electricity demand in Québec | 192 |
| `historique-production-electricite-quebec` | History of generation by source | 59,915 |
| `production-electricite-quebec` | Current sources of electricity generated | 48 |
| `historique-production-consommation-ec-horaire` | Hourly generation and consumption (framework agreement method) | 61,375 |
| `historique-production-consommation-proxy-horaire` | Hourly generation and consumption (proxy method) | 61,371 |
| `importations-exportations-avec-transits` | Imports and exports per market, incl. wheel-through | 48 |

## Steps

1. **Confirm the field names first.** Call `getDataset` on `/catalog/datasets/{dataset_id}` and
   read `fields`. Field names are French and differ per dataset — do not assume them. Verified
   examples:
   - `historique-demande-electricite-quebec` → `date` (datetime), `moyenne_mw` (double)
   - `production-electricite-quebec` → `date`, `valeurs_total`, `valeurs_hydraulique`,
     `valeurs_eolien`, `valeurs_solaire`, `valeurs_thermique`, `valeurs_autres` (all double)

2. **Query records** — call `getRecords` on `/catalog/datasets/{dataset_id}/records`. Build the
   query from the ODSQL clauses, all of which are declared parameters on the operation:
   - `select` — projection and expressions
   - `where` — filtering
   - `group_by` — aggregation buckets
   - `order_by` — sorting
   - `limit` / `offset` — paging
   - `timezone` — evaluate date functions in a chosen zone rather than UTC

3. **Filter by time in the `where` clause** using the ODSQL date functions the platform
   documents: `year()`, `month()`, `day()`, `hour()`, `minute()`, `second()`, `now()`,
   `date_format()`. In v2.1 these return **integers**, not strings — a `where` clause written
   against v2.0 that compared them to quoted strings will silently stop matching.

4. **Aggregate server-side instead of paging.** Combine `select` with an aggregation and
   `group_by` on a date function to get, for example, a monthly mean of `moyenne_mw` in one call.
   This is the single biggest efficiency win on the 50k–60k-row history datasets: bucket on the
   server, transfer tens of rows instead of tens of thousands.

5. **Read one row** — call `getRecord` on `/catalog/datasets/{dataset_id}/records/{record_id}`
   using the `_id` returned by `getRecords`.

6. **Enumerate categories before filtering** — for the datasets with categorical columns, call
   `getRecordsFacets` with `facet=<field>` to see the real values rather than guessing labels.

## Rules

- **Two hourly series exist and they are not interchangeable.**
  `historique-production-consommation-ec-horaire` uses the framework-agreement method;
  `historique-production-consommation-proxy-horaire` uses a proxy method. They have nearly
  identical record counts and will diverge in value. Pick one, name it in your output, and do
  not mix them in a single chart.
- **Aggregation key formats changed in v2.1.** Date aggregation keys come back as ISO-format
  dates; in v2.0 they were timestamps. Parse accordingly.
- **`group_by` on geo fields is deprecated** — use `geo_cluster()`.
- The records endpoint caps how many records a single query returns; the exports endpoints do
  not. If you find yourself paging past a few thousand rows, switch to the bulk-export skill.
- Division by zero in an ODSQL arithmetic expression returns `null`, not an error. Guard derived
  ratios (e.g. renewable share) with `ifnull()`.
- Every call is `GET` and therefore idempotent — retry freely, but govern retries with
  `X-RateLimit-Remaining` / `X-RateLimit-Reset` rather than an idempotency key. There is none,
  because there are no writes.
- On `400`, read `error_code` and `message`: `ODSQLSyntaxError` reports the character position
  and the clause containing the error.
- Attribute Hydro-Québec and note any modification when you publish these series (CC BY-NC 4.0,
  non-commercial only).
