---
name: Submit quote and risk data to Beazley
description: Feed a quote or risk record from a partner system into Beazley's core Record of Risk systems using the Data Capture API v2, including the lock-state handshake that protects concurrent edits.
api: openapi/beazley-data-capture-quote-and-risk-data-v2.yml
generated: '2026-07-25'
method: generated
operations:
  - 55f2b5dc97fe1e075c26d7c4   # GET  /ping/            — ping
  - 55f2b5dc97fe1e075c26d7c2   # POST /risks/           — create risk
  - 55f2b5dc97fe1e075c26d7c5   # GET  /risks/{id}       — risk
  - 55f2b5dc97fe1e075c26d7c7   # PUT  /risks/{id}       — update risk
  - 55f2b5dc97fe1e075c26d7c3   # GET  /lockstate/{id}   — lockstate
  - 55f2b5dc97fe1e075c26d7c6   # PUT  /lockstate/{id}   — update lockstate
---

# Submit quote and risk data to Beazley

Beazley's Data Capture API is the only write path Beazley publishes: it is, in Beazley's own words,
"a channel for partner systems to feed quote and risk data directly into Beazley's core Record of
Risk systems." Use **v2** (`https://api.beazley.com/riskcapture/v2`). v1 is still published but v2 is
current and is the only version with the lock-state resource.

## Before you start

- **You need an approved key.** Auth is an Azure API Management subscription key sent as the
  `Ocp-Apim-Subscription-Key` header (or the `subscription-key` query parameter). A developer account
  at `https://developer.beazley.com/signup` is self-serve; the subscription is not — the *Policy Data
  Submission - Production* product is `approvalRequired=true`. Ask ITArchitecture@Beazley.com.
- **Develop against the sandbox first.** Beazley's own spec text says to. Use
  `https://api.beazley.com/sandbox/riskcapture/v2` under the *Policy Data Submission - Development*
  product (`openapi/beazley-data-capture-quote-and-risk-data-v2-sandbox.yml`, same operation shapes).
- **Budget your calls.** Policy Data Submission allows 100 calls/minute up to 10,000 calls/week
  (`rate-limits/beazley-rate-limits.yml`).
- **There is no idempotency key.** Nothing in the contract dedupes a retried `POST /risks/`. Keep
  your own correlation identifier inside the risk payload and reconcile with `GET /risks/{id}` before
  retrying a write you are unsure about. See `conventions/beazley-conventions.yml`.

## Steps

1. **Verify the subscription.** `GET /ping/` (operation `55f2b5dc97fe1e075c26d7c4`). A 401 with
   `WWW-Authenticate: AzureApiManagementKey` means the key is missing, wrong, or the subscription has
   not been approved yet. Do not proceed until ping succeeds.
2. **Create the risk.** `POST /risks/` (operation `55f2b5dc97fe1e075c26d7c2`) with the quote/risk
   body agreed with Beazley. Success is **201**; `400` is a rejected payload. Capture the identifier
   Beazley returns — it is the `{id}` for every later call.
   > The request body has **no declared schema** in the published OpenAPI. The payload shape is
   > agreed bilaterally with Beazley during onboarding. Do not invent fields; use the payload
   > Beazley supplies.
3. **Read it back.** `GET /risks/{id}` (operation `55f2b5dc97fe1e075c26d7c5`) to confirm what landed
   in the Record of Risk before you show anything to an underwriter or broker.
4. **Take the lock before you update.** `GET /lockstate/{id}` (operation `55f2b5dc97fe1e075c26d7c3`)
   to read the current lock, then `PUT /lockstate/{id}` (operation `55f2b5dc97fe1e075c26d7c6`) to
   claim it. Beazley uses an explicit lock resource here instead of ETag/If-Match — there is no
   conditional-request support anywhere in the catalog.
5. **Update the risk.** `PUT /risks/{id}` (operation `55f2b5dc97fe1e075c26d7c7`). Declared responses
   are `201`, `400` and `422`; treat `422` as a semantic rejection of the risk data (not a transport
   fault) and surface it to the user rather than retrying.
6. **Release the lock.** `PUT /lockstate/{id}` again to clear it, so the next system — or a Beazley
   underwriter working the same record — is not blocked.

## Error handling

- `400` — malformed payload. Fix and resend; do not retry unchanged.
- `422` — the payload parsed but was rejected on content (Data Capture v2 update only).
- `401` — key missing/invalid/unapproved. Never retry in a loop; it will not resolve itself.
- `404`/`500` — the response is the Azure APIM envelope `{"statusCode": n, "message": "..."}`, not
  RFC 9457 problem+json. See `errors/beazley-problem-types.yml`.

## What this API cannot do

Beazley does not publish bind, policy issuance or FNOL operations. Risk capture ends at the Record of
Risk; binding happens in the gated myBeazley broker portal and claims are notified by web form and
email. Do not promise an end-to-end quote-to-bind flow over this API.
