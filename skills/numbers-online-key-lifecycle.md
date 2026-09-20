---
generated: '2026-09-19'
method: generated
name: Sign up, fund and rotate API keys safely
description: 'Account bootstrap for an agent or operator: mint a key with no card, check balance and usage, add prepaid credit, mint narrowed keys, rotate in place with a grace window, and understand which actions are one-way.'
api: openapi/numbers-online-openapi.yml
operations:
- accountSignup
- getAccount
- accountTopup
- listAccountKeys
- createAccountKey
- rotateAccountKey
- updateAccountKey
- getSigning
source: Grounded in openapi/numbers-online-openapi.yml (operationIds verified) and the provider docs; rules cite conventions/, errors/, rate-limits/ and authentication/.
---

# Sign up, fund and rotate API keys safely

## Steps
1. **Create an account and first key** — `accountSignup` (`POST /api/v1/account/signup`, NO key, 3/hour per IP) with `{}` or `{ "email": "…" }` (email only for renewal reminders). The response carries `api_key` (`nol_…`) exactly once; store it now — keys are kept only as SHA-256 hashes and the key + account UUID is the identity, with no recovery path. New accounts start on the free tier with a zero balance.
2. **Check balance and usage** — `getAccount` (`GET /api/v1/account`): `balance_micros`, trailing-30-day usage, key inventory (display fields only), tenants.
3. **Add prepaid credit when you need to burst past the free pool** — `accountTopup` (`POST /api/v1/account/topup`) with `{ "amount_cents": 2000 }` ($5 minimum 500 – $500 maximum 50000); returns a Stripe Checkout session; credit applies on payment confirmation. Billed endpoints return `402 insufficient_balance` (with `topup_url`) when the balance is exhausted.
4. **Mint narrowed keys** — `listAccountKeys` / `createAccountKey` (`GET`/`POST /api/v1/account/keys`, `manage` use case). A minted key can hold only a subset of the minter's use cases — give a PBX or webhook key just `lookup`, an agent key `mcp`.
5. **Rotate in place** — `rotateAccountKey` (`POST /api/v1/account/keys/{id}/rotate`) with `{ "grace_seconds": 0..86400 }`. Same key id, billing identity, rate buckets and HKDF signing secret; the old key keeps working for the grace window (default and maximum 24 h; `0` kills it immediately after a leak). The new raw key is returned once.
6. **Rename or disable** — `updateAccountKey` (`PATCH /api/v1/account/keys/{id}`) with `{ "name" }` or `{ "disabled": true }`. **Disabling is ONE-WAY** — rotate or mint instead of trying to re-enable; disabling the last enabled account-level key is refused with 409.
7. **Operator signing (optional)** — `getSigning` (`GET /api/v1/account/signing`) returns the key's derived HMAC secret and scheme for signed surfaces such as `/api/v1/sbc/redirect`; signed requests MUST use the long `/api/v1/*` path.

## Reversibility summary
Rotation is reversible inside its grace window; disable is not; there is no delete for keys, tenants or bound numbers. See `conventions/numbers-online-conventions.yml` → `reversibility`.
