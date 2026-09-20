---
generated: '2026-09-19'
method: generated
name: Assess an inbound caller and file a receipt-backed report
description: 'Answer-time caller intelligence for a voice agent, chatbot or CRM: get a signed, PII-safe risk read on an inbound number, act on it as an advisory signal, and optionally spend the single-use receipt on a community report. Verify signatures offline.'
api: openapi/numbers-online-openapi.yml
operations:
- inboundLookup
- reportNumber
- getReceipt
- publicKey
source: Grounded in openapi/numbers-online-openapi.yml (operationIds verified) and the provider docs; rules cite conventions/, errors/, rate-limits/ and authentication/.
---

# Assess an inbound caller and file a receipt-backed report

Use when a call or message arrives and the agent wants context before it answers. Every field is a supplementary, low-confidence signal — the agent keeps the routing decision.

## Auth
- `Authorization: Bearer nol_…` (or `X-API-Key`). The key needs the `inbound_lookup` use case (every self-service key has it); `report` needs an ACCOUNT-level key (tenant sub-keys cannot report). See `authentication/numbers-online-authentication.yml`.

## Steps
1. **Look the caller up** — `inboundLookup` (`POST /api/v1/inbound/lookup`) with `{ "number": "+14155551212", "context": "inbound_voice" | "inbound_sms" }`; pass the call's STIR/SHAKEN `verstat` / `attestation` when you have it. Read `identity_type` (verified_business | verified_individual | unverified | unknown), `display_label` (never a personal name), `risk.level`, `recommended_action`, `signals`, and keep `receipt_id`. Known and unknown numbers return the same 200 shape. Billed $0.004 on the standard tier; pooled 429 + `Retry-After`; 402 when prepaid balance is exhausted.
2. **Apply your own policy** — treat `risk` as advisory. Never state a call is "safe", "spam" or lawful; never make an eligibility decision on it (Terms §6, FCRA exclusion).
3. **Optionally report the number** — `reportNumber` (`POST /api/v1/report`) with `{ "e164": "<same number>", "tags": ["robocall"], "receipt_id": "<from step 1>" }`. Tags only, no free text. The receipt is single-use: a stale/used/mismatched one returns `409 receipt_invalid`; over-quota returns 429 (10/day free, +100/day per verified business number).
4. **Verify the evidence later** — `getReceipt` (`GET /api/v1/receipts/{id}`, no key needed — the id is the capability) returns `signed_payload` + `response_signature` (`ed25519:<base64>`) and `number_hash = sha256(E.164)`; fetch the SPKI PEM once from `publicKey` (`GET /api/v1/publickey`) and verify offline. Treat a receipt id as sensitive: the hash binds to a specific number.

## Fail-open rule
On a live call path a slow or failed lookup must advance the call unchanged — use a short timeout and proceed with no signal. The endpoint itself returns a neutral body on internal errors.

## Errors and retries
Flat JSON `{ error, code }`; switch on `code` (`errors/numbers-online-problem-types.yml`). `inboundLookup` has no Idempotency-Key — do not blind-retry a billed dip; on 429 wait `Retry-After`.
