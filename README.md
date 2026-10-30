# Hydro-Québec

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

**Areas:** Energy · Canada · Utilities · Electricity · Grid · Energy Markets · Renewables · Open Data · Demand Response · Carbon

## Hydro-Québec on APIs.io

Everything profiled for Hydro-Québec is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/hydro-quebec/](https://apis.io/providers/hydro-quebec/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [Hydro-Québec Open Data Search API v1](https://apis.io/apis/hydro-quebec/hydro-quebec-open-data-search-api-v1/) — The legacy Opendatasoft Search API v1 still served on the Hydro-Québec open data portal. Verified live and anonymous on 2026-07-27 — GET…
- [Hydro-Québec Catalog API](https://apis.io/apis/hydro-quebec/hydro-quebec-catalog-api/) — API to enumerate datasets
- [Hydro-Québec Dataset API](https://apis.io/apis/hydro-quebec/hydro-quebec-dataset-api/) — API to work on records

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [opendatasoft](https://apis.io/servers/hydro-quebec/opendatasoft/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Hydro Quebec Agentic Access](https://apis.io/agentic-access/hydro-quebec/hydro-quebec-agentic-access/)

#### Collections (2)

Postman and Open Collection request collections.

- [Explore API](https://apis.io/collections/hydro-quebec/open-hydro-quebec-open-data-explore-api-v2-0/)
- [Explore API](https://apis.io/collections/hydro-quebec/open-hydro-quebec-open-data-explore-api-v2-1/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Hydro Quebec Open Data Explore Api V2 0 Overlay](https://apis.io/overlays/hydro-quebec/hydro-quebec-open-data-explore-api-v2-0-overlay/)
- [Hydro Quebec Open Data Explore Api V2 1 Overlay](https://apis.io/overlays/hydro-quebec/hydro-quebec-open-data-explore-api-v2-1-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Hydro Quebec Authentication](https://apis.io/security/hydro-quebec/hydro-quebec-authentication/)
- [Hydro Quebec Domain Security](https://apis.io/security/hydro-quebec/hydro-quebec-domain-security/)
- [Hydro Quebec Vulnerability Disclosure](https://apis.io/security/hydro-quebec/hydro-quebec-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Hydro Quebec Scopes](https://apis.io/scopes/hydro-quebec/hydro-quebec-scopes/)

#### Rate limits (1)

Published request limits.

- [Hydro Quebec Rate Limits](https://apis.io/rate-limits/hydro-quebec/hydro-quebec-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.hydroquebec.com/)
- [Documentation](https://www.hydroquebec.com/documents-data/open-data/)
- [Getting started](https://help.opendatasoft.com/apis/ods-explore-v2/explore_v2.1.html#section/Getting-Started)
- [API reference](https://donnees.hydroquebec.com/api/v2/console)
- [Support](https://www.hydroquebec.com/sefco2016/en/open-data-contact-us.html)
- [Blog](https://news.hydroquebec.com/en/)
- [Security](https://donnees.hydroquebec.com/.well-known/security.txt)
- [Terms of service](https://www.hydroquebec.com/terms-confidentiality.html)
- [Privacy policy](https://www.hydroquebec.com/documents-data/act-respecting-access/protection-personal-information/)
- [Status](https://status.huwise.com/)

## API Evangelist rating

**Kin Score 51.8** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 51.4 |
| Contract governance | 4.5 |
| Operational transparency | 65.8 |
| Developer ergonomics | 66.1 |
| Access clarity | 21.1 |

**Agent readiness 44.3** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | na |
| MCP Server | verified |
| Auth Clarity | bearer (partial credit) |
| Idempotency | na |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | na |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 45.9** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/hydro-quebec/](https://apis.io/providers/hydro-quebec/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Hydro-Québec: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/hydro-quebec/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
