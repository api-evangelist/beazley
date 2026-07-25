---
name: Run a Beazley compliance check and pull its audit trail
description: Execute a rule-driven compliance validation against Beazley's compliance engine, search brokers/agencies/product lines, and retrieve the audit record of what was checked.
api: openapi/beazley-compliance-web-api.yml
generated: '2026-07-25'
method: generated
operations:
  - 5893134739845516588448cc   # POST /health         — healthcheck
  - 5893134739845516588448c8   # POST /check          — check
  - 5893134739845516588448c9   # POST /search         — search
  - 5893134739845516588448ca   # POST /report         — report
  - 5893134739845516588448cb   # POST /audit/lookups  — getauditlookups
  - 5893134739845516588448cd   # GET  /audit          — getauditentry
---

# Run a Beazley compliance check and pull its audit trail

`https://api.beazley.com/compliance/v1` is the only Beazley API with typed schemas. It runs the
rule-driven compliance validation that sits behind Beazley's underwriting systems and keeps an audit
trail of every check performed.

## Before you start

- Key: `Ocp-Apim-Subscription-Key`, from the *Compliance* product (`approvalRequired=true`).
- Allowance: **10 calls/minute, 10,000 calls/week** — the tightest budget in the catalog. Batch your
  checks; do not call per keystroke.
- This API offers four representations (`application/json`, `text/json`, `application/xml`,
  `text/xml`) on every operation. Send `Accept: application/json` unless you have a reason not to.
- There is no sandbox twin for Compliance. Development and production are the same surface.

## Steps

1. **Health check first.** `POST /health` (operation `5893134739845516588448cc`) with a
   `HealthCheckQuery` body. It reports across the validation engine and its databases — a failing
   dependency explains a `500` far better than a retry does.
2. **Run the validation.** `POST /check` (operation `5893134739845516588448c8`) with a
   `ComplianceCheckQuery` — `Input` (the thing being validated) plus `Parameters` (the system and
   action that select which rules run). The response is a `ComplianceCheckResult`:
   - `Valid` — the overall verdict.
   - `Identifier` — keep this; it is your handle on the check in the audit trail.
   - `Details[]` — per-rule `ComplianceResultDetail` with `Type`, `SubType`, `CategoryCode` and
     nested `Items`, `Errors` and `Warnings`.
   - `IsAsync` / `Deferred[]` — **some rules do not resolve inline.** If `IsAsync` is true or
     `Deferred` is non-empty, the verdict is provisional; reconcile later through the audit trail
     rather than treating `Valid` as final.
3. **Read the messages properly.** `Errors[]` and `Warnings[]` are `ComplianceMessage` objects with
   `Message`, `Category`, `Code` (integer) and `Source`. Key your own handling on `Code` +
   `Category`, not on the free-text `Message`.
4. **Search reference data.** `POST /search` (operation `5893134739845516588448c9`) with a
   `ComplianceSearchQuery` — `Type` selects the entity (broker agencies, broker contacts, product
   lines) and `Query` carries the criteria. Results come back as untyped objects; treat the shape as
   Type-dependent.
5. **Get the report.** `POST /report` (operation `5893134739845516588448ca`) returns the audit report
   of the compliance checks that were performed — the artefact to file against a submission.
6. **Reconcile against the audit trail.** `POST /audit/lookups` (operation
   `5893134739845516588448cb`) resolves the lookup registries (`AuditLookupQuery.Key`), then
   `GET /audit?query.id=<id>` (operation `5893134739845516588448cd`) returns `AuditEntry` records —
   `Id`, `Timestamp`, `System`, `Action`, `User`, `Data`, `MetaData`. Paged searches use
   `AuditQuery` with `Page`, `Size` and a `Filter`; `AuditResult` returns `TotalCount` alongside
   `Entries`, so unlike the marketing API you can page deterministically here.

## Error handling

Every operation declares `200` and `500` only — there is no declared 4xx. A malformed query is
therefore most likely to surface as a `500` with the APIM envelope
`{"statusCode": 500, "message": "..."}`. Validate your `ComplianceCheckQuery` against the declared
schema before sending, and log `Identifier` on every call so a `500` can still be traced through the
audit trail.
