# Beazley (beazley)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Beazley plc is a London-headquartered specialty insurer and one of the largest managing agents at Lloyd's of London, underwriting through Lloyd's syndicates alongside US admitted and surplus lines carriers and a European company platform. Its book is specialty property and casualty — cyber and technology risks (where it is a global market leader), professional indemnity, management liability and directors and officers, marine, political risk, contingency, environmental, healthcare and property. Its home market is the United Kingdom, where there is no open-insurance mandate; the only market-wide data and API modernization effort is the Lloyd's Blueprint Two programme, and Beazley sat on the closed beta group that tested Lloyd's ACORD-based Core Data Record. Unusually for a carrier, Beazley operates a real first-party developer portal at developer.beazley.com — an Azure API Management portal with self-serve account signup, a publicly browsable catalog of 14 published APIs across nine families, sandbox environments, and machine-readable OpenAPI 3.0.1 for every one of them.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/beazley/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/beazley/refs/heads/main/apis.yml)

## Tags

- Insurance
- United Kingdom
- Property and Casualty
- Cyber Insurance
- Specialty Insurance
- Lloyd's of London
- Underwriting
- Risk Data
- Broker
- Carrier

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## API Posture

Open to browse, gated to call. The developer portal at [https://developer.beazley.com](https://developer.beazley.com) is a genuine self-serve Azure API Management portal (HTTP 200), not a login wall and not a marketing page: the catalog is publicly browsable, signup is email-and-password with a proof-of-work captcha, and OpenAPI 3.0.1 is exportable anonymously for all 14 published APIs. But every one of the nine APIM products is `subscriptionRequired` **and** `approvalRequired`, and the live gateway at `https://api.beazley.com` returns HTTP 401 with `WWW-Authenticate: AzureApiManagementKey` — so a working subscription key still requires Beazley to approve you.

The APIs are partner- and broker-oriented, not consumer-facing. On the four insurance verbs:

| Verb | Exposed | Where |
| --- | --- | --- |
| Quote | Partial | `Data Capture: Quote and Risk Data` v1/v2/v3 feeds quote and risk data into Beazley's core Record of Risk systems; `Simple Raters` exposes `POST /Cyber` but is self-described as "for testing" |
| Bind | No | Brokers bind through the gated myBeazley "quote and bind platform" (login wall), not through a documented API |
| Issue | No | No policy issuance or policy administration endpoint is published |
| FNOL | No | Claims are notified by web form and email; there is no claims API |

**ACORD posture:** no ACORD reference found in the developer portal or specs. A grep for ACORD, AL3, ACORD XML, NGDS, IVANS, Vertafore and Applied Epic across all 14 harvested specs and the full APIM API/product metadata returned zero hits. ACORD reaches Beazley only indirectly, at market level, through Lloyd's Blueprint Two Core Data Record — which Lloyd's states is based on ACORD Standards and whose closed beta group named Beazley. That is programme participation, not a published interface.

**Auth:** Azure APIM subscription key (`Ocp-Apim-Subscription-Key` header or `subscription-key` query parameter). No OAuth2, no OIDC — `/.well-known/openid-configuration` and `/.well-known/oauth-authorization-server` both fall through to the site 404 page.

**Not found:** webhooks, event catalog, AsyncAPI, GraphQL, gRPC, public Postman collection or workspace.

## APIs

### Beazley Data Capture: Quote and Risk Data v2

The current published version of Beazley's risk data capture API. Provides a channel for partner systems to feed quote and risk data directly into Beazley's core Record of Risk systems, with create, read and update of risk records plus a lock-state resource for concurrency control.

- **Human URL:** [https://developer.beazley.com/api-details#api=55f2b5dc97fe1e150ca5aedb](https://developer.beazley.com/api-details#api=55f2b5dc97fe1e150ca5aedb)
- **Base URL:** `https://api.beazley.com/riskcapture/v2`

#### Properties

- [OpenAPI](openapi/beazley-data-capture-quote-and-risk-data-v2.yml)
- [OpenAPI (Sandbox)](openapi/beazley-data-capture-quote-and-risk-data-v2-sandbox.yml)
- [Documentation](https://developer.beazley.com/apis)

### Beazley Data Capture: Quote and Risk Data v1

The original version of the risk data capture API, superseded by v2 but still published with its own sandbox environment.

- **Human URL:** [https://developer.beazley.com/api-details#api=54af9d8897fe1e0c48fd377f](https://developer.beazley.com/api-details#api=54af9d8897fe1e0c48fd377f)
- **Base URL:** `https://api.beazley.com/riskcapture/v1`

#### Properties

- [OpenAPI](openapi/beazley-data-capture-quote-and-risk-data.yml)
- [OpenAPI (Sandbox)](openapi/beazley-data-capture-quote-and-risk-data-sandbox.yml)

### Beazley Data Capture: Quote and Risk Data v3 (pre-release)

A pre-release version published under Beazley's Prerelease product, exposing a single create-risk operation backed by an Azure Logic App.

- **Human URL:** [https://developer.beazley.com/api-details#api=5964d64cf815b002d0231152](https://developer.beazley.com/api-details#api=5964d64cf815b002d0231152)
- **Base URL:** `https://api.beazley.com/prerelease/riskcapture/v3`

#### Properties

- [OpenAPI](openapi/beazley-data-capture-quote-and-risk-data-v3-pre-release.yml)

### Beazley Compliance Web API

Rule-driven compliance checks, search over broker agencies, broker contacts and product lines, audit reporting of compliance checks performed, audit lookup registries, and a system health check.

- **Human URL:** [https://developer.beazley.com/api-details#api=58931347398455121c4a697f](https://developer.beazley.com/api-details#api=58931347398455121c4a697f)
- **Base URL:** `https://api.beazley.com/compliance/v1`

#### Properties

- [OpenAPI](openapi/beazley-compliance-web-api.yml)

### Beazley Broker and Insured Marketing Data v2

Marketing details for Beazley's partner organisations — broker and insured organisations, contacts and microsites.

- **Human URL:** [https://developer.beazley.com/api-details#api=562e100f8097920dd41ffaa0](https://developer.beazley.com/api-details#api=562e100f8097920dd41ffaa0)
- **Base URL:** `https://api.beazley.com/marketing/v2`

#### Properties

- [OpenAPI](openapi/beazley-broker-and-insured-marketing-data-v2.yml)
- [OpenAPI (Sandbox)](openapi/beazley-broker-and-insured-marketing-data-v2-sandbox.yml)

### Beazley Currency Exchange

A standard set of foreign exchange rates for Beazley systems — rates, rate providers and supported currencies.

- **Human URL:** [https://developer.beazley.com/api-details#api=56d08a2b97fe1e18e889da30](https://developer.beazley.com/api-details#api=56d08a2b97fe1e18e889da30)
- **Base URL:** `https://api.beazley.com/fx/v1`

#### Properties

- [OpenAPI](openapi/beazley-currency-exchange.yml)
- [OpenAPI (Sandbox)](openapi/beazley-currency-exchange-sandbox.yml)

### About Beazley

Reference data on Beazley's people and divisions, sold through the Beazley Public Data product at up to 1,000 calls per hour.

- **Human URL:** [https://developer.beazley.com/api-details#api=55392e7f97fe1e0510faf7bf](https://developer.beazley.com/api-details#api=55392e7f97fe1e0510faf7bf)
- **Base URL:** `https://api.beazley.com/about/v1`

#### Properties

- [OpenAPI](openapi/beazley-about-beazley.yml)
- [OpenAPI (Sandbox)](openapi/beazley-about-beazley-sandbox.yml)

### Beazley Fast Reader

Insurance glossary and knowledge API — definitions of insurance terms, FAQs by intent name, and product lookup by term. Published sandbox-only.

- **Human URL:** [https://developer.beazley.com/api-details#api=5967575d6e0029dd58e53203](https://developer.beazley.com/api-details#api=5967575d6e0029dd58e53203)
- **Base URL:** `https://api.beazley.com/sandbox/fastreader/v1`

#### Properties

- [OpenAPI](openapi/beazley-fast-reader.yml)

### Beazley Simple Raters

A single cyber rating operation (`POST /Cyber`), described by Beazley as a set of "super-simple raters for testing".

- **Human URL:** [https://developer.beazley.com/api-details#api=5804a8868097920fbc0ae7e9](https://developer.beazley.com/api-details#api=5804a8868097920fbc0ae7e9)
- **Base URL:** `https://api.beazley.com/hack/raters/v1`

#### Properties

- [OpenAPI](openapi/beazley-simple-raters.yml)

## Common Properties

- [Website](https://www.beazley.com/)
- [Developer Portal](https://developer.beazley.com/)
- [Documentation](https://developer.beazley.com/apis)
- [Sign Up](https://developer.beazley.com/signup)
- [Products / Plans](https://developer.beazley.com/products)
- [Broker Centre](https://www.beazley.com/en-us/broker-centre)
- [LinkedIn](https://www.linkedin.com/company/beazley)

## Corporate Note

Beazley plc is subject to a recommended all-cash offer from Zurich Insurance Group, announced under Rule 2.7 of the UK Takeover Code on 2 March 2026.

## Review

See [review.yml](review.yml) for the full API Evangelist reviewer finding, including every probed URL with its HTTP status and the provenance of all 14 harvested specifications.
