---
generated: '2026-09-19'
method: generated
name: Run multi-tenant PBX or SBC customers under one prepaid balance
description: 'The MSP control plane for resellers and PBX operators: create tenants, issue lookup-only sub-keys per customer, manage per-tenant suppression lists, and disable/re-enable tenants — all billing against the single account balance.'
api: openapi/numbers-online-openapi.yml
operations:
- createTenant
- listTenants
- getTenant
- issueTenantKey
- addTenantSuppression
- listTenantSuppressions
- removeTenantSuppression
- setTenantStatus
source: Grounded in openapi/numbers-online-openapi.yml (operationIds verified) and the provider docs; rules cite conventions/, errors/, rate-limits/ and authentication/.
---

# Run multi-tenant PBX or SBC customers under one prepaid balance

## Auth
- ACCOUNT-level key only; a tenant sub-key cannot manage tenants, top up, enrol or report.

## Steps
1. **Create a tenant per downstream customer / site** — `createTenant` (`POST /api/v1/account/tenants`) with `{ "name": "Dental office" }`. Usage, billing rollups, rate limits and suppression lists are attributed per tenant while all spend draws on the one balance. `listTenants` / `getTenant` return trailing-30-day usage and sub-key counts.
2. **Issue the tenant's credential** — `issueTenantKey` (`POST /api/v1/account/tenants/{id}/keys`) with `{ "name": "Front desk PBX" }`. The sub-key inherits the account tier, can perform lookups / SBC redirect / pre-call only (a PBX credential, not an account credential), and the raw key is returned exactly once. Put it in that tenant's FreeSWITCH/Kamailio/3CX config.
3. **Suppress numbers per tenant** — `addTenantSuppression` (`POST /api/v1/account/tenants/{id}/suppressions`) with `{ "number": "+14155552671", "label": "front desk" }`. A suppressed number gets no enrichment and no charge through that tenant's sub-keys; numbers are stored as SHA-256 hashes and never returned — `listTenantSuppressions` shows labels + timestamps only. Reverse with `removeTenantSuppression` (`DELETE` the same number).
4. **Pause or resume a customer** — `setTenantStatus` (`PATCH /api/v1/account/tenants/{id}`) with `{ "status": "disabled" | "active" }`. Disabling also disables all of the tenant's sub-keys (they fail authentication); re-enabling restores them. There is no tenant delete.

## Notes
Agent (MCP) usage rolls up per tenant the same way if the agent uses the tenant's sub-key, and tenant suppression lists apply to agent lookups too. Rate limits: `rate-limits/numbers-online-rate-limits.yml`; errors: `errors/numbers-online-problem-types.yml`.
