---
name: Compute Québec electricity carbon intensity
description: Combine Hydro-Québec's direct GHG emission factors with the generation-mix and import/export series to derive an emissions figure for Québec electricity — using only published factors.
api: openapi/hydro-quebec-open-data-explore-api-v2-1-openapi.json
base_url: https://donnees.hydroquebec.com/api/explore/v2.1
operations: [getDataset, getRecords, getRecordsFacets, exportRecords]
generated: '2026-07-27'
method: generated
---

# Compute Québec electricity carbon intensity

Hydro-Québec publishes both halves of the calculation: the emission factors and the generation
and trade volumes. This skill joins them without inventing a factor.

## The datasets

| dataset_id | What it is | Records |
|---|---|---|
| `facteurges` | Direct GHG emission factors by energy source, per market | 14 |
| `facteurs-directs-ges` | Same subject, near-duplicate entry | 0 |
| `estimation-emissions-directes-ges` | Hydro-Québec's own estimate of direct GHG emissions from electricity use in Québec | 48 |
| `production-electricite-quebec` | Sources of electricity generated in Québec | 48 |
| `historique-production-electricite-quebec` | History of generation by source | 59,915 |
| `importations-exportations-avec-transits` | Imports and exports per market, incl. wheel-through | 48 |

## Steps

1. **Load the emission factors** — call `getRecords` on
   `/catalog/datasets/facteurges/records`. Verified fields: `sources_d_energie` (text) plus one
   double column per market — `quebec`, `ontario`, `nouveau_brunswick`, `new_york`,
   `nouvelle_angleterre`, `miso`, `pjm`. Only 14 rows, so fetch them all in one call.

2. **Confirm the units from the dataset metadata.** Call `getDataset` on
   `/catalog/datasets/facteurges` and read `metas.default.description` and the field labels
   before doing any arithmetic. **Do not assume g CO₂e/kWh** — carry through whatever unit
   Hydro-Québec states, and label it in your output.

3. **Load the generation mix** — call `getRecords` on
   `/catalog/datasets/production-electricite-quebec/records`. Verified fields: `date` (datetime),
   `valeurs_total`, `valeurs_hydraulique`, `valeurs_eolien`, `valeurs_solaire`,
   `valeurs_thermique`, `valeurs_autres` (all double). The named sources map onto the
   `sources_d_energie` rows in `facteurges` — enumerate them with `getRecordsFacets`
   (`facet=sources_d_energie`) rather than hand-mapping from memory.

4. **Bring in trade** — call `getRecords` on
   `/catalog/datasets/importations-exportations-avec-transits/records`. Imported electricity
   carries the emission factor of its *source market*, which is why `facteurges` has a column per
   market (New York, New England, Ontario, New Brunswick, MISO, PJM). Wheel-through energy
   transits Québec and should not be attributed to Québec consumption.

5. **Aggregate on the server.** Use `select` with an aggregation plus `group_by` on a date
   function to produce annual or monthly totals in one call rather than paging
   `historique-production-electricite-quebec` (59,915 rows). For a full history, use
   `exportRecords` in Parquet instead.

6. **Cross-check against Hydro-Québec's own estimate.** Pull
   `estimation-emissions-directes-ges` and compare. If your derived figure diverges materially
   from the published estimate, report the published estimate and flag the divergence — do not
   quietly ship your own number as Hydro-Québec's.

## Rules

- **`facteurges` and `facteurs-directs-ges` are near-duplicate catalog entries with the same
  title.** `facteurs-directs-ges` reported `records_count` 0 on 2026-07-27; `facteurges` had 14
  rows. Check `records_count` via `getDataset` and use the populated one. Name the exact
  `dataset_id` you used in your output.
- **These are *direct* emission factors.** They are not lifecycle or embodied-carbon factors.
  Never relabel them as such.
- Field names are French; labels are mixed French and English. Read them from `dataset.fields`
  rather than transliterating.
- Division by zero returns `null` in ODSQL — wrap any intensity ratio with `ifnull()` so an empty
  interval does not silently poison an average.
- All operations are `GET` and idempotent. Govern retries with `X-RateLimit-Remaining` and
  `X-RateLimit-Reset`; on `429` back off to the `reset_time` in the body.
- CC BY-NC 4.0. If you publish a carbon-intensity figure derived from this data, cite
  Hydro-Québec as the source of the factors, state that you computed the result, link the
  licence, and keep the use non-commercial. The licence explicitly forbids suggesting that
  Hydro-Québec endorses your derivation.
