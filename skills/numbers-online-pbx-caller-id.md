---
generated: '2026-09-19'
method: generated
name: Label inbound calls on a PBX or softphone with caller name and risk
description: 'The PBX/softphone flow: resolve a caller name (CNAM) and an optional risk tag for an inbound call using the plain-text CID endpoint or the JSON lookup, batch-enrich contact lists, and refresh caches from the reputation-change feed within the 30-day contractual bound.'
api: openapi/numbers-online-openapi.yml
operations:
- cidLookup
- lookupNumber
- lookupNumberBatch
- lookupChanges
source: Grounded in openapi/numbers-online-openapi.yml (operationIds verified) and the provider docs; rules cite conventions/, errors/, rate-limits/ and authentication/.
---

# Label inbound calls on a PBX or softphone with caller name and risk

## Auth
- Key with the `lookup` use case. Header-less PBX clients (FreeSWITCH mod_cidlookup, Asterisk dialplan) may use `?key=` on the CID endpoint only — use a dedicated, rotated key because it can land in access logs.

## Steps
1. **Plain-text caller ID (simplest)** — `cidLookup` (`GET /api/v1/cid/{number}?key=…&country=US&spam_tag=Spam?&spam_threshold=80`). ALWAYS `text/plain`: the body is the name (`ACME CORP`), the tagged name when the signal crosses your threshold (`Spam? ACME CORP`), or the literal `UNAVAILABLE` on no-name, auth, balance or rate-limit failure (HTTP status still meaningful). Paste the body verbatim as the caller name. Loose national / `00`-prefixed input is accepted. Billed like a lookup; unresolvable numbers are free.
2. **JSON lookup (richer)** — `lookupNumber` (`GET /api/v1/lookup/{e164}` with `?verstat=` and `?max_cache_age=` optional). Use `formatted`, `line_type`, `carrier` (range allocation, not porting-aware), `country`, `cnam`, `verstat`, `spam_score` (1–99, may be null) and `risk{score, level, model}`. Invalid input is `200 valid:false` and unbilled. Send an `Idempotency-Key` so a retry is not double-billed; `X-Billed-Micros` / `X-Billing-Endpoint` show what the call cost.
3. **Enrich a list** — `lookupNumberBatch` (`POST /api/v1/lookup/batch`) with `{ "numbers": [ …≤100 ] }`; results in input order plus a billing summary; whole-batch 402 precheck; `Idempotency-Key` supported. This is a list surface, not a call-path surface (can take seconds).
4. **Keep caches fresh** — poll `lookupChanges` (`GET /api/v1/lookup/changes?since=<cursor>&limit=1000`) and re-dip only the numbers you care about; an entry is a refresh HINT, not proof of movement. Regardless of hints, Terms §7 requires cached responses to be refreshed or dropped within 30 days, and corrected/removed records dropped on the next refresh.

## Fail-open rule
Set a sub-second timeout on the call path; on timeout fall back to the raw number. Only prefix a risk word above a threshold you choose — the signal is advisory and a missing name means "unknown", not negative. Personal numbers verified on Numbers Online never return a name.

## Errors
`errors/numbers-online-problem-types.yml`; 429 → honour `Retry-After` (free pool 10/min · 50/day, +60/min · +2,000/day per verified business number; 60/min per key otherwise).
