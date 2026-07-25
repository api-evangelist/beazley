---
name: Look up Beazley reference data (FX, people, insurance terms)
description: Convert currency with Beazley's FX rates, resolve Beazley people and divisions with a deletion feed for downstream sync, and answer insurance-terminology questions from the Fast Reader glossary.
api: openapi/beazley-currency-exchange.yml
generated: '2026-07-25'
method: generated
operations:
  - 56d08a2b97fe1e081ca252f5   # GET /rates       — Rates            (Currency Exchange)
  - 56d08a2b97fe1e081ca252f6   # GET /providers   — Providers        (Currency Exchange)
  - 56d08a2b97fe1e081ca252f7   # GET /currencies  — Currencies       (Currency Exchange)
  - 55392e7f97fe1e0ff06f4256   # GET /people                 — people             (About Beazley)
  - 55392e7f97fe1e0ff06f4257   # GET /people/{rid}           — person by ID       (About Beazley)
  - 55392e7f97fe1e0ff06f4258   # GET /people/profileimage    — profileimage by ID (About Beazley)
  - 55392e7f97fe1e0ff06f4255   # GET /People/deleted/        — deleted people     (About Beazley)
  - 596757de398455123cd32ae7   # GET /definitions            — definition by term (Fast Reader)
  - 5971dd5476b7b3f0e01a426f   # GET /definitions/           — definitions        (Fast Reader)
  - 5972212f109c6c8fce68fc40   # GET /faqs                   — FAQ by intent      (Fast Reader)
  - 59675bb966f3f16555c931b0   # GET /faqs/                  — FAQs               (Fast Reader)
  - 59675c4259efa7b3b8c0fa3b   # GET /products/{term}        — products           (Fast Reader)
related_apis:
  - openapi/beazley-about-beazley.yml
  - openapi/beazley-fast-reader.yml
---

# Look up Beazley reference data

Three read-only families, three different APIM products, three different call budgets. All are GET,
all are keyed with `Ocp-Apim-Subscription-Key`, and all are safe to cache aggressively.

## Currency Exchange — `https://api.beazley.com/fx/v1`

*Reference Services - Production* product: 100 calls/minute, 10,000 calls/week.

1. `GET /currencies` (operation `56d08a2b97fe1e081ca252f7`) — the supported currency list. Cache it;
   it changes rarely.
2. `GET /providers` (operation `56d08a2b97fe1e081ca252f6`) — the rate providers Beazley sources from.
   Pin one provider in your integration so your figures are reproducible.
3. `GET /rates` (operation `56d08a2b97fe1e081ca252f5`) — the workhorse. Parameters: `scurr` (source),
   `dcurr` (destination), `bcurr` (base), `startdate`, `enddate`, `provider`, `amount`, `divby`.
   Passing `amount` makes the API do the conversion for you; passing a `startdate`/`enddate` range
   returns a series, which is what you want for a policy period rather than a spot date.
   Sandbox twin: `https://api.beazley.com/sandbox/fx/v1`.

## About Beazley — `https://api.beazley.com/about/v1`

*Beazley Public Data* product: up to 1,000 calls/hour — the most generous budget Beazley publishes.

1. `GET /people` (operation `55392e7f97fe1e0ff06f4256`) — filter by `division`,
   `firstNameFragment`, `lastNameFragment`, or `since` for records changed after a timestamp.
2. `GET /people/{rid}` (operation `55392e7f97fe1e0ff06f4257`) — a single person by record id.
3. `GET /people/profileimage?id=` (operation `55392e7f97fe1e0ff06f4258`) — the profile image.
4. `GET /People/deleted/?since=` (operation `55392e7f97fe1e0ff06f4255`) — **the deletion feed.** This
   is the correct way to keep a downstream directory in sync: poll `/people?since=` for changes and
   `/People/deleted/?since=` for removals. It is the only tombstone feed anywhere in the Beazley
   catalog — do not infer deletions by diffing collections.
   Note the capital P in `/People/deleted/`; the other person paths are lowercase.
   Sandbox twin: `https://api.beazley.com/sandbox/about/v1`, which additionally exposes
   `GET /people/profileimagebyemail/`.

## Fast Reader — `https://api.beazley.com/sandbox/fastreader/v1`

*Prerelease* product, published **sandbox-only** with no call allowance stated. It is backed by an
Azure Logic App and its operations take an explicit `Content-Type` header parameter.

1. `GET /definitions?term=` (operation `596757de398455123cd32ae7`) — an insurance-term definition.
   It declares a **`204`** as well as `200`: an unknown term returns no content, not a 404. Handle
   the empty case explicitly.
2. `GET /definitions/` (operation `5971dd5476b7b3f0e01a426f`) — the whole glossary (also `200`/`204`).
3. `GET /faqs?intentName=` (operation `5972212f109c6c8fce68fc40`) and `GET /faqs/` (operation
   `59675bb966f3f16555c931b0`) — FAQ lookup by intent name, which is the seam for wiring this into a
   chatbot or agent.
4. `GET /products/{term}` (operation `59675c4259efa7b3b8c0fa3b`) — Beazley product lookup by term.

> Beazley's own spec says the FAQ and product features are "coming soon", and the whole API sits
> under Prerelease. Treat it as unstable: do not build a customer-facing glossary on it without
> caching a local copy.

## Caching and etiquette

None of these APIs sends cache headers or rate-limit headers, and none supports conditional requests.
Cache on your side by TTL, prefer the `since`/`UpdatedSince` delta parameters over re-pulling, and
keep well inside the per-product allowances in `rate-limits/beazley-rate-limits.yml`.
