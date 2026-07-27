---
name: Bulk export a Hydro-Québec dataset
description: Pull an entire Hydro-Québec dataset — including the multi-million-row weather and vegetation datasets — through the uncapped export endpoints instead of paging the records endpoint.
api: openapi/hydro-quebec-open-data-explore-api-v2-1-openapi.json
base_url: https://donnees.hydroquebec.com/api/explore/v2.1
operations: [getDataset, listDatasetExportFormats, exportRecords, exportRecordsCSV, exportRecordsParquet, exportRecordsGPX, listExportFormats, exportDatasets, exportCatalogCSV, exportCatalogDCAT]
generated: '2026-07-27'
method: generated
---

# Bulk export a Hydro-Québec dataset

The records endpoint is capped. The export endpoints are documented as having **no
limitation**. For anything beyond a few thousand rows, export — do not page.

## When to use this

Check `metas.default.records_count` from `getDataset` first. Datasets that must be exported:

| dataset_id | Records |
|---|---|
| `historique-donnees-meteo` | 2,326,547 |
| `calendrier-travaux-degagement-distribution-shap` | 649,019 |
| `historique-consommation-secteur-activite-mun-mois` | 637,207 |
| `donnees-hydrometeorologiques` | 294,317 |
| `historique-production-electricite-quebec` | 59,915 |
| `historique-consommation-secteur-activite-mrc-mois` | 52,437 |
| `donnees-hydrometriques` | 51,484 |

## Steps

1. **Discover the formats the dataset actually supports** — call `listDatasetExportFormats` on
   `/catalog/datasets/{dataset_id}/exports`. Do not assume; geospatial formats are only offered
   where the dataset has geometry. The platform's format enum is `csv`, `fgb`, `geojson`, `gpx`,
   `json`, `jsonl`, `jsonld`, `kml`, `n3`, `ov2`, `parquet`, `rdfxml`, `shp`, `turtle`, `xlsx`.

2. **Export** — pick the operation that matches your target:
   - `exportRecords` on `/catalog/datasets/{dataset_id}/exports/{format}` — generic, any
     supported format
   - `exportRecordsParquet` on `.../exports/parquet` — **use this for the large analytical
     datasets**; columnar and far smaller on the wire than CSV
   - `exportRecordsCSV` on `.../exports/csv`
   - `exportRecordsGPX` on `.../exports/gpx` — geospatial only

3. **Shape the export before it leaves the server.** The export operations accept the same ODSQL
   clauses as `getRecords`, and in v2.1 `group_by` is available on export endpoints too. Apply
   `select`, `where` and `group_by` so you download the slice you need rather than 2.3M raw rows.

4. **Set the export parameters** the spec declares:
   - `limit_export` — cap the export size deliberately
   - `use_labels` — emit human-readable column labels instead of field names
   - `compressed` — gzip the response; use it on anything over a few MB
   - `epsg` — reproject geometry for the geospatial exports

5. **Export the catalog, not the records**, when you want an inventory rather than data:
   - `listExportFormats` on `/catalog/exports`
   - `exportCatalogCSV` on `/catalog/exports/csv`
   - `exportCatalogDCAT` on `/catalog/exports/dcat{dcat_ap_format}` — RDF/XML with DCAT and
     DCAT-AP namespaces, the machine-readable description of all 26 datasets

## Rules

- **CSV exports emit a UTF-8 BOM by default** in v2.1. Strip it or open with a BOM-aware reader,
  or your first column name will arrive with a leading `﻿`.
- **GPX exports use `<extension>` rather than `<desc>`** for attributes in v2.1. Parsers written
  against v2.0 output will drop the attributes silently.
- **Datetimes in GeoJSON exports are ISO-format strings** in v2.1; they were integer timestamps
  in v2.0.
- The `-json` and `-shap` vegetation datasets are the same planning data in different formats.
  Export the `-shap` variant only if you need geometry.
- Exports are `GET` and idempotent — a failed or truncated download can be re-requested safely.
  Still, read `X-RateLimit-Remaining` before firing several large exports in a loop, and back off
  to the `X-RateLimit-Reset` timestamp on `429` (`errorcode` 10002).
- Responses are `Cache-Control: no-store` with no `ETag`, so there is no conditional-request path.
  Track `metas.default.modified` on the dataset and re-export only when it moves.
- Publish under CC BY-NC 4.0: cite Hydro-Québec, flag modifications, link the licence, no
  commercial use.
