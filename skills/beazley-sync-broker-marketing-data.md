---
name: Sync broker and insured marketing data
description: Page and delta-sync Beazley's partner organisations, contacts and microsites out of the Broker and Insured Marketing Data v2 API, and write contact and organisation changes back.
api: openapi/beazley-broker-and-insured-marketing-data-v2.yml
generated: '2026-07-25'
method: generated
operations:
  - 562e100f809792165c5ef92c   # GET  /ping/                          — ping
  - 562e100f809792165c5ef92a   # GET  /organisations                  — organisations
  - 562e100f809792165c5ef929   # GET  /organisations/{id}             — organisation by id
  - 562e100f809792165c5ef928   # PUT  /organisations/{id}             — organisation update
  - 562e100f809792165c5ef924   # GET  /contacts                       — contacts
  - 562e100f809792165c5ef923   # GET  /contacts/{id}                  — contact by id
  - 562e100f809792165c5ef921   # POST /contacts/                      — create contact
  - 562e100f809792165c5ef922   # PUT  /Contacts/{id}                  — update contact
  - 562e100f809792165c5ef926   # GET  /organisations/{id}/contacts    — contacts by organisation
  - 562e100f809792165c5ef927   # GET  /microsites/                    — microsites
  - 562e100f809792165c5ef925   # GET  /microsites/{id}/contacts       — contacts by microsite
  - 562e100f809792165c5ef92b   # GET  /microsites/{id}/organisations  — organisations by microsite
---

# Sync broker and insured marketing data

`https://api.beazley.com/marketing/v2` holds the marketing detail for Beazley's partner
organisations — brokers and insureds, their contacts, and the microsites they belong to. This is the
only Beazley family that paginates and the only one designed for incremental sync.

## Before you start

- Key: `Ocp-Apim-Subscription-Key`, from the *Marketing Data - Production* product
  (`approvalRequired=true`). Sandbox twin: `https://api.beazley.com/sandbox/marketing/v2` under
  *Marketing Data - Development*.
- **Every operation is scoped by `ProviderID`** (query parameter). You will be told yours at
  onboarding; without it you are not addressing your own data.
- Allowance: 10 calls/minute, 10,000 calls/week. That is tight — page in bulk, do not fan out.

## Steps

1. **Ping.** `GET /ping/` (operation `562e100f809792165c5ef92c`) to prove the key and subscription.
2. **Full pull, paged.** `GET /organisations` (operation `562e100f809792165c5ef92a`) with
   `ProviderID`, `PageNumber` and `RecordsPerPage`. Walk `PageNumber` until a short page comes back —
   the contract declares no total-count or next-link field, so page exhaustion is your only stop
   signal. Do the same for `GET /contacts` (operation `562e100f809792165c5ef924`).
3. **Narrow instead of scanning.** `GET /organisations` also filters on `AccessCode`, `Domain` and
   `ThirdPartyOrgRef` — use `ThirdPartyOrgRef` to reconcile against your own CRM ids and `Domain` to
   resolve an insured from an email domain, rather than pulling the whole book.
4. **Delta sync on the next run.** Re-issue the same collection calls with `UpdatedSince` set to the
   timestamp of your last successful run. This is the intended incremental path and the only way to
   stay inside the weekly quota.
   > There is **no deletion feed** in the marketing family (unlike About Beazley, which publishes
   > one). A record that stops appearing is your only deletion signal, so a periodic full pull is
   > still needed to detect removals.
5. **Walk the hierarchy when you need context.** `GET /microsites/` (operation
   `562e100f809792165c5ef927`) lists microsites; `GET /microsites/{id}/organisations` (operation
   `562e100f809792165c5ef92b`) and `GET /microsites/{id}/contacts` (operation
   `562e100f809792165c5ef925`) scope by microsite; `GET /organisations/{id}/contacts` (operation
   `562e100f809792165c5ef926`) scopes contacts to one organisation.
6. **Write back.** Create a contact with `POST /contacts/` (operation `562e100f809792165c5ef921`),
   update one with `PUT /Contacts/{id}` (operation `562e100f809792165c5ef922` — note the capital C in
   the path, it differs from the GET path casing), update an organisation with
   `PUT /organisations/{id}` (operation `562e100f809792165c5ef928`). Read the record back with
   `GET /contacts/{id}` / `GET /organisations/{id}` afterwards; there is no idempotency key, so a
   read-back is the only way to confirm a retried write did not double-apply.

## Gotchas

- Path casing is inconsistent (`/contacts/{id}` for GET, `/Contacts/{id}` for PUT). Follow the spec
  literally per operation.
- Request and response bodies have **no declared schemas** in the published OpenAPI — only the
  parameters are typed. Agree payload shapes with Beazley (ITArchitecture@Beazley.com) and validate
  defensively.
- No `PageNumber`/`RecordsPerPage` defaults are documented; always send both explicitly.
