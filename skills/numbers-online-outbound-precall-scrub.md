---
generated: '2026-09-19'
method: generated
name: Scrub a destination before dialing and enrol your caller ID for call-provenance
description: 'The outbound flow for dialers, SBCs and AI voice agents: verify and enrol your own business number once, then run the free pre-call check on every destination to read the first-party do-not-contact preference, dial risk and cost estimate. NO_MATCH is not consent.'
api: openapi/numbers-online-openapi.yml
operations:
- accountVerifyPhoneStart
- accountVerifyPhoneConfirm
- precallEnroll
- accountPhonesList
- accountPhonePatch
- precallLookup
source: Grounded in openapi/numbers-online-openapi.yml (operationIds verified) and the provider docs; rules cite conventions/, errors/, rate-limits/ and authentication/.
---

# Scrub a destination before dialing and enrol your caller ID for call-provenance

## Auth
- Account-level key with the `precall` use case for enrollment; any key with `precall` for the check. Tenant sub-keys cannot enrol (403).

## One-time setup: bind and enrol your calling number
1. **Start verification** — `accountVerifyPhoneStart` (`POST /api/v1/account/verify-phone/start`) with `{ "phone": "+14155550142", "channel": "voice" | "sms" }`. Returns 429 + `Retry-After` on cooldown.
2. **Confirm the code** — `accountVerifyPhoneConfirm` (`POST /api/v1/account/verify-phone/confirm`) with `{ "phone", "code" }`. Free accounts may bind exactly one number (402 `paid_verification_required` otherwise); a number already claimed elsewhere returns 409. A verified BUSINESS number also raises the account's pooled limits.
3. **Enrol it** — `precallEnroll` (`POST /api/v1/outbound/enroll`) with `{ "number": "+14155550142", "enrolled": true }`. Enrolment is an attestation that this number only dials after a pre-call check; it is **revocable** with `enrolled: false`. The same toggle is resource-shaped: `accountPhonesList` (`GET /api/v1/account/phones`) then `accountPhonePatch` (`PATCH /api/v1/account/phones/{e164}`) with `{ "precall_enrolled": true|false }`.

## Every dial: the pre-call check
4. **Check the destination** — `precallLookup` (`POST /api/v1/outbound/lookup`) with `{ "from": "<your enrolled number>", "to": "<destination>", "context": "outbound_voice" | "outbound_sms" }`. Read:
   - `dnc`: `SUPPRESS` (verified owner asked not to be contacted on this channel — remove), `NO_MATCH` (no preference on record — **not consent**), `UNKNOWN`. This is the first-party owner preference, NOT the government DNC registry (`compliance` is the separate licensed signal and stays `unknown` until a partner is configured).
   - `dial_risk` (0–100 + level + `structural_type` such as intl_premium / premium_prs / satellite) — the cost/abuse risk of DIALING, not of the callee.
   - `cost_estimate` — indicative retail voice per-minute and SMS per-message list prices, not a quote.
   - `provenance_recorded` / `edge_id` when `from` is enrolled: a hashed (from → to) edge kept 7 days that later shields your number from reports about calls you did not place.
   Free, bundled, fail-open: treat any error as `UNKNOWN` and proceed under your own lawful basis. Fair-use pool 429 + `Retry-After`.
5. **Re-scrub** — Terms §8: scrub results are one-time use; re-scrub lists at least every 31 days. For lists rather than single dials use `v1Scrub` (`POST /api/v1/scrub`, up to 1,000 numbers, `Idempotency-Key` supported).

## Rules
Your consent records and registry checks still govern whether the call goes out; the API never asserts a call is compliant. The original `/api/v1/precall/lookup` and `/api/v1/precall/enroll` paths are permanent aliases of steps 3–4.
