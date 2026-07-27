---
name: Discover Hydro-Québec open datasets
description: Find which of Hydro-Québec's 26 public datasets holds the data you need, read its field schema, and confirm its size before querying.
api: openapi/hydro-quebec-open-data-explore-api-v2-1-openapi.json
base_url: https://donnees.hydroquebec.com/api/explore/v2.1
operations: [getDatasets, getDatasetsFacets, getDataset, getRecordsFacets, getDatasetAttachments, exportCatalogDCAT]
generated: '2026-07-27'
method: generated
---

# Discover Hydro-Québec open datasets

Always start here. Every other Hydro-Québec skill needs a `dataset_id`, and guessing one
returns `404 NotFoundResource`.

## Before you start

- No credentials. The catalog is public — send the request with no key.
- Only `GET` is supported. Every call is safe to retry.
- Data is licensed **CC BY-NC 4.0**: attribute Hydro-Québec, state whether you modified the
  data, link the licence, and do not use it commercially.

## Steps

1. **List the catalog** — call `getDatasets` on `/catalog/datasets`. Use `limit` (and `offset`)
   to page; the response gives `total_count`, `results` and `_links`. There are 26 datasets, so
   `limit=30` returns the whole catalog in one call.

2. **Search by keyword** — pass a `where` clause with ODSQL. The full-text functions are
   `search()`, `suggest()` and `startswith()`. Filter on the metadata fields exposed under
   `metas.default` — `title`, `description`, `theme`, `modified`, `records_count`.

3. **Narrow by theme** — call `getDatasetsFacets` on `/catalog/facets` with `facet=theme` to
   enumerate the three Hydro-Québec themes and their dataset counts:
   *Electricity consumption*, *Infrastructure and grid*,
   *GHG emissions and the energy transition*. Then re-run `getDatasets` with `refine` set to the
   theme value you want.

4. **Read the dataset's schema** — call `getDataset` on `/catalog/datasets/{dataset_id}`. This
   is the step people skip. The Explore API models record fields as untyped
   `additionalProperties`, so the **only** way to know a dataset's column names and types is
   `dataset.fields` from this call. Example: `historique-demande-electricite-quebec` has exactly
   two fields, `date` (datetime) and `moyenne_mw` (double).

5. **Check the size before you query** — read `metas.default.records_count` from the same
   response and branch:
   - under a few thousand records → page with `getRecords`
   - hundreds of thousands or more → go straight to the bulk-export skill.
     `historique-donnees-meteo` is 2,326,547 records; `calendrier-travaux-degagement-distribution-shap`
     is 649,019.

6. **Enumerate a field's values** — call `getRecordsFacets` on
   `/catalog/datasets/{dataset_id}/facets` with `facet=<field>` to see the distinct values and
   their counts before writing a `where` filter.

7. **Look for documentation files** — call `getDatasetAttachments` on
   `/catalog/datasets/{dataset_id}/attachments`. Methodology notes and source files are attached
   here, not in the description.

8. **Snapshot the whole catalog** — call `exportCatalogDCAT` on
   `/catalog/exports/dcat{dcat_ap_format}` for an RDF/XML DCAT description of all 26 datasets,
   including `dcterms:modified`. This is the machine-readable inventory to diff against on a
   schedule.

## Rules

- **Never invent a `dataset_id`.** Resolve it from `getDatasets`. The slugs are French,
  kebab-case, and carry meaningful suffixes: `-json` / `-shap` are the same data in different
  formats, and `-ra-mois` / `-mrc-mois` / `-mun-mois` are the same series at administrative
  region, MRC and municipality granularity.
- Two dataset pairs are near-duplicates in the live catalog — `facteurges` /
  `facteurs-directs-ges`, and the `-json` / `-shap` vegetation pairs. Read `records_count` before
  choosing; several duplicates report 0 records.
- Read `X-RateLimit-Remaining` and `X-RateLimit-Reset` from the response headers. On `429`, back
  off until the `X-RateLimit-Reset` timestamp — it is formatted `YYYY-MM-DD HH:MM:SS+00:00`, not
  epoch seconds.
- Errors return `{"error_code": "...", "message": "..."}`, not RFC 9457 problem+json. `400`
  `ODSQLSyntaxError` names the offending clause and character position — read it, do not retry
  blindly. See `errors/hydro-quebec-problem-types.yml`.
- Responses set `Cache-Control: no-store` and return no `ETag` or `Last-Modified`. Cache locally
  against the dataset's `metas.default.modified` instead of issuing conditional requests.
- Use `/api/explore/v2.1`. The `/api/explore/v2.0` base path still works but returns
  `ODS-Explore-API-Deprecation` on every response.
