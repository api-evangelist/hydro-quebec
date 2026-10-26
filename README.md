# Hydro-Québec (hydro-quebec)

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
