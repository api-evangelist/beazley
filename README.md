# Beazley

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

Beazley plc is a London-headquartered specialty insurer and one of the largest managing agents at Lloyd's of London, underwriting through Lloyd's syndicates alongside US admitted and surplus lines carriers and a European company platform. Its book is specialty property and casualty — cyber and technology risks (where it is a global market leader), professional indemnity, management liability and directors and officers, marine, political risk, contingency, environmental, healthcare and property. Its home market is the United Kingdom, where there is no open-insurance mandate; the only market-wide data and API modernization effort is the Lloyd's Blueprint Two programme, and Beazley sat on the closed beta group that tested Lloyd's ACORD-based Core Data Record. Unusually for a carrier, Beazley operates a real first-party developer portal at developer.beazley.com — an Azure API Management portal with self-serve account signup, a publicly browsable catalog of 14 published APIs across nine families, sandbox environments, and machine-readable OpenAPI 3.0.1 for every one of them. The APIs are partner-and-broker oriented rather than consumer facing — risk and quote data capture into Beazley's core Record of Risk systems, broker and insured marketing data, compliance validation, currency exchange, a cyber rater, and insurance-terms reference data. Every API is behind an Azure APIM subscription key and every product carries approvalRequired, so browsing and spec download are open but actually calling the gateway requires Beazley to approve the subscription. There is no ACORD, AL3 or IVANS reference anywhere in the portal or the specs, no webhook or event catalog, no GraphQL, and no bind, issue or FNOL endpoint — bind is done by brokers through the gated myBeazley quote-and-bind portal, not through the public API surface. Beazley is subject to a recommended all-cash offer from Zurich Insurance Group announced 2 March 2026.

**Areas:** Insurance · United Kingdom · Property and Casualty · Cyber Insurance · Specialty Insurance · Lloyd's of London · Underwriting · Risk Data · Carrier

## Beazley on APIs.io

Everything profiled for Beazley is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/beazley/](https://apis.io/providers/beazley/)** — or go straight to one of the APIs or properties below.

### APIs (19)

- [Beazley Audit API](https://apis.io/apis/beazley/beazley-audit-api/) — The Audit API from Beazley — 2 operation(s) for audit.
- [Beazley Check API](https://apis.io/apis/beazley/beazley-check-api/) — The Check API from Beazley — 1 operation(s) for check.
- [Beazley Contacts API](https://apis.io/apis/beazley/beazley-contacts-api/) — The Contacts API from Beazley — 4 operation(s) for contacts.
- [Beazley Currencies API](https://apis.io/apis/beazley/beazley-currencies-api/) — The Currencies API from Beazley — 1 operation(s) for currencies.
- [Beazley Cyber API](https://apis.io/apis/beazley/beazley-cyber-api/) — The Cyber API from Beazley — 1 operation(s) for cyber.
- [Beazley Definitions API](https://apis.io/apis/beazley/beazley-definitions-api/) — The Definitions API from Beazley — 2 operation(s) for definitions.
- [Beazley Health API](https://apis.io/apis/beazley/beazley-health-api/) — The Health API from Beazley — 1 operation(s) for health.
- [Beazley Lockstate API](https://apis.io/apis/beazley/beazley-lockstate-api/) — The Lockstate API from Beazley — 1 operation(s) for lockstate.
- [Beazley Microsites API](https://apis.io/apis/beazley/beazley-microsites-api/) — The Microsites API from Beazley — 3 operation(s) for microsites.
- [Beazley Organisations API](https://apis.io/apis/beazley/beazley-organisations-api/) — The Organisations API from Beazley — 4 operation(s) for organisations.
- [Beazley People API](https://apis.io/apis/beazley/beazley-people-api/) — The People API from Beazley — 5 operation(s) for people.
- [Beazley Ping API](https://apis.io/apis/beazley/beazley-ping-api/) — The Ping API from Beazley — 1 operation(s) for ping.
- [Beazley Products API](https://apis.io/apis/beazley/beazley-products-api/) — The Products API from Beazley — 1 operation(s) for products.
- [Beazley Providers API](https://apis.io/apis/beazley/beazley-providers-api/) — The Providers API from Beazley — 1 operation(s) for providers.
- [Beazley Rates API](https://apis.io/apis/beazley/beazley-rates-api/) — The Rates API from Beazley — 1 operation(s) for rates.
- [Beazley Report API](https://apis.io/apis/beazley/beazley-report-api/) — The Report API from Beazley — 1 operation(s) for report.
- [Beazley Risks API](https://apis.io/apis/beazley/beazley-risks-api/) — The Risks API from Beazley — 2 operation(s) for risks.
- [Beazley Search API](https://apis.io/apis/beazley/beazley-search-api/) — The Search API from Beazley — 1 operation(s) for search.
- [Beazley Faqs API](https://apis.io/apis/beazley/beazley-faqs-api/) — The Faqs API from Beazley — 2 operation(s) for faqs.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [beazley](https://apis.io/servers/beazley/beazley/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Beazley Agentic Access](https://apis.io/agentic-access/beazley/beazley-agentic-access/)

#### Collections (14)

Postman and Open Collection request collections.

- [About Beazley](https://apis.io/collections/beazley/open-beazley-about-beazley/)
- [About Beazley (Sandbox)](https://apis.io/collections/beazley/open-beazley-about-beazley-sandbox/)
- [Broker and Insured Marketing Data v2](https://apis.io/collections/beazley/open-beazley-broker-and-insured-marketing-data-v2/)
- [Broker and Insured Marketing Data v2 (Sandbox)](https://apis.io/collections/beazley/open-beazley-broker-and-insured-marketing-data-v2-sandbox/)
- [Compliance Web API](https://apis.io/collections/beazley/open-beazley-compliance-web-api/)
- [Currency Exchange](https://apis.io/collections/beazley/open-beazley-currency-exchange/)
- [Currency Exchange (Sandbox)](https://apis.io/collections/beazley/open-beazley-currency-exchange-sandbox/)
- [Data Capture: Quote and Risk Data](https://apis.io/collections/beazley/open-beazley-data-capture-quote-and-risk-data/)
- [Data Capture: Quote and Risk Data (Sandbox)](https://apis.io/collections/beazley/open-beazley-data-capture-quote-and-risk-data-sandbox/)
- [Data Capture: Quote and Risk Data v2](https://apis.io/collections/beazley/open-beazley-data-capture-quote-and-risk-data-v2/)
- [Data Capture: Quote and Risk Data v2 (Sandbox)](https://apis.io/collections/beazley/open-beazley-data-capture-quote-and-risk-data-v2-sandbox/)
- [Data Capture: Quote and Risk Data v3 (pre-release)](https://apis.io/collections/beazley/open-beazley-data-capture-quote-and-risk-data-v3-pre-release/)
- [Fast Reader](https://apis.io/collections/beazley/open-beazley-fast-reader/)
- [Simple Raters](https://apis.io/collections/beazley/open-beazley-simple-raters/)

#### Overlays (9)

OpenAPI overlays, including conversational phrasing for each operation.

- [Beazley About Beazley Overlay](https://apis.io/overlays/beazley/beazley-about-beazley-overlay/)
- [Beazley Compliance Overlay](https://apis.io/overlays/beazley/beazley-compliance-overlay/)
- [Beazley Currency Exchange Overlay](https://apis.io/overlays/beazley/beazley-currency-exchange-overlay/)
- [Beazley Data Capture V1 Overlay](https://apis.io/overlays/beazley/beazley-data-capture-v1-overlay/)
- [Beazley Data Capture V2 Overlay](https://apis.io/overlays/beazley/beazley-data-capture-v2-overlay/)
- [Beazley Data Capture V3 Overlay](https://apis.io/overlays/beazley/beazley-data-capture-v3-overlay/)
- [Beazley Fast Reader Overlay](https://apis.io/overlays/beazley/beazley-fast-reader-overlay/)
- [Beazley Marketing V2 Overlay](https://apis.io/overlays/beazley/beazley-marketing-v2-overlay/)
- [Beazley Simple Raters Overlay](https://apis.io/overlays/beazley/beazley-simple-raters-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Beazley Authentication](https://apis.io/security/beazley/beazley-authentication/)
- [Beazley Domain Security](https://apis.io/security/beazley/beazley-domain-security/)
- [Beazley Trust Center](https://apis.io/security/beazley/beazley-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Beazley Plans](https://apis.io/plans/beazley/beazley-plans/)

#### Rate limits (1)

Published request limits.

- [Beazley Rate Limits](https://apis.io/rate-limits/beazley/beazley-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.beazley.com/)
- [Documentation](https://developer.beazley.com/apis)
- [API reference](https://developer.beazley.com/apis)
- [Sign up](https://developer.beazley.com/signup)
- [Compliance](https://trust.beazley.security/)
- [Terms of service](https://developer.beazley.com/products)
- [Privacy policy](https://www.beazley.com/en-us/privacy-and-cookies-statements/)
- [GitHub](https://github.com/beazley)

## API Evangelist rating

**Kin Score 48.5** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 79.5 |
| Contract quality | 43.1 |
| Contract governance | 4.5 |
| Operational transparency | 34.2 |
| Developer ergonomics | 51.8 |
| Access clarity | 71.1 |

**Agent readiness 32.9** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
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
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 22.8** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/beazley/](https://apis.io/providers/beazley/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Beazley: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/beazley/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
