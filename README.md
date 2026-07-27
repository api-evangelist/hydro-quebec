# Hydro-Québec (hydro-quebec)

Hydro-Québec is the government-owned Crown corporation that generates, transmits and distributes almost all of the electricity consumed in Québec, Canada — a vertically integrated, near-monopoly utility running one of the largest hydroelectric fleets in the world and serving roughly 4.6 million customer accounts across the province. It sits at every point of the value chain at once, as generator, transmission owner, distributor and retailer, plus a cross-border exporter into the New England and New York markets. Its API posture is a clean split. Market and grid data is genuinely open — a public Opendatasoft-powered portal at donnees.hydroquebec.com serves 26 datasets (electricity demand and generation, imports and exports, outages, GHG emission factors, hydrometric and weather data, winter peak demand events, vegetation control) through a documented, anonymously callable REST API with a machine-readable OpenAPI 3.0.3 description and a DCAT catalog export, licensed CC BY-NC 4.0. Consumer data is closed — there is no documented customer-facing API, no Green Button Download My Data or Connect My Data service, and no third-party consent flow; a customer's own usage is reachable only by logging into the Espace client web portal. Québec has no consumer energy data right. Ontario's Green Button regulation (O. Reg. 633/21 under the Electricity Act, 1998) is province-specific and does not bind Hydro-Québec, and Canada has no national equivalent to Australia's Consumer Data Right energy regime. Open market data, closed consumer data, no mandate.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/hydro-quebec/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/hydro-quebec/refs/heads/main/apis.yml)

## Tags

- Energy
- Canada
- Utilities
- Electricity
- Grid
- Energy Markets
- Renewables
- Open Data
- Demand Response
- Carbon

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### Hydro-Québec Open Data Explore API v2.1

Read-only REST API over Hydro-Québec's 26 public open datasets — catalog search, dataset metadata, record query with the Opendatasoft Query Language (ODSQL), facets, attachments, and bulk exports to CSV, Parquet, GPX and DCAT. Covers Québec electricity demand and generation, imports and exports, ongoing outages and planned service interruptions, direct GHG emission factors, hydrometric and weather history, winter peak demand events, and vegetation control planning. Verified callable anonymously with no API key (HTTP 200, 26 datasets returned, 2026-07-27); an optional `apikey` query parameter is supported for authenticated requests. Data is licensed CC BY-NC 4.0 (attribution, non-commercial). Market and grid data only — no individual customer consumption is exposed.

- **Human URL:** [https://donnees.hydroquebec.com/api/v2/console](https://donnees.hydroquebec.com/api/v2/console)
- **Base URL:** `https://donnees.hydroquebec.com/api/explore/v2.1`

#### Tags

- Open Data
- Electricity
- Grid
- Energy Markets
- Carbon

#### Properties

- [OpenAPI](openapi/hydro-quebec-open-data-explore-api-v2-1-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://www.hydroquebec.com/documents-data/open-data/)
- [API Reference](https://donnees.hydroquebec.com/api/v2/console)
- [Portal](https://donnees.hydroquebec.com/pages/accueil/)
- [Licensing](https://www.hydroquebec.com/documents-data/open-data/licence.html)

### Hydro-Québec Open Data Explore API v2.0

The prior major version of the Hydro-Québec open data Explore API, still served alongside v2.1 at its own base path and described by its own OpenAPI 3.0.3 document (also mirrored at `/api/v2/swagger.json`). Same 16 read-only endpoints — catalog, datasets, records, facets, attachments and exports — over the same 26 public datasets. Anonymously callable, optional `apikey` query parameter, CC BY-NC 4.0.

- **Human URL:** [https://donnees.hydroquebec.com/api/v2/console](https://donnees.hydroquebec.com/api/v2/console)
- **Base URL:** `https://donnees.hydroquebec.com/api/explore/v2.0`

#### Tags

- Open Data
- Electricity
- Grid
- Energy Markets

#### Properties

- [OpenAPI](openapi/hydro-quebec-open-data-explore-api-v2-0-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://www.hydroquebec.com/documents-data/open-data/)
- [API Reference](https://donnees.hydroquebec.com/api/v2/console)
- [Licensing](https://www.hydroquebec.com/documents-data/open-data/licence.html)

### Hydro-Québec Open Data Search API v1

The legacy Opendatasoft Search API v1 still served on the Hydro-Québec open data portal. Verified live and anonymous on 2026-07-27 — `GET /api/datasets/1.0/search/` returned HTTP 200 with all 26 datasets. Documented through the portal's interactive v1 API console. Hydro-Québec publishes no OpenAPI or Swagger description for this version (`/api/v1/swagger.json` returns HTTP 404), so no machine-readable contract was harvested for it.

- **Human URL:** [https://donnees.hydroquebec.com/api/v1/console](https://donnees.hydroquebec.com/api/v1/console)
- **Base URL:** `https://donnees.hydroquebec.com/api/datasets/1.0`

#### Tags

- Open Data
- Electricity
- Legacy

#### Properties

- [API Reference](https://donnees.hydroquebec.com/api/v1/console)
- [Documentation](https://www.hydroquebec.com/documents-data/open-data/)
- [Licensing](https://www.hydroquebec.com/documents-data/open-data/licence.html)

## Common Properties

- [Website](https://www.hydroquebec.com/)
- [Portal](https://donnees.hydroquebec.com/pages/accueil/)
- [Documentation](https://www.hydroquebec.com/documents-data/open-data/)
- [Licensing](https://www.hydroquebec.com/documents-data/open-data/licence.html)
- [LinkedIn](https://www.linkedin.com/company/hydro-quebec)

## Maintainers

- **Kin Lane** — kin@apievangelist.com
