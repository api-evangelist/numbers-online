# Numbers Online

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Numbers Online is a phone-number trust and intelligence service operated by Evergrow Management Pte. Ltd. of Singapore. It runs a free public reverse phone lookup with a community-driven, advisory spam-risk score, paid number verification for people and businesses, and a B2B API keyed on a single E.164 primitive: parsing and validation, single and batch lookup (line type, range carrier, CNAM, STIR/SHAKEN verstat and a low-confidence spam signal), signed inbound caller intelligence with Ed25519 receipts, an outbound pre-call do-not-contact scrub and call-provenance enrollment, consent-first list scrubbing, a ClearIP-compatible SBC/SIP redirect decision, a multi-tenant MSP control plane, and a hosted read-only MCP server plus Vapi/Retell webhooks for AI voice agents. The 56-operation REST API is published as an OpenAPI 3.0.3 contract at /api/spec, with an llms.txt, an A2A agent card at /.well-known/agent-card.json, markdown mirrors of the docs, and a self-service free tier with no card.

**Areas:** Phone Intelligence · Caller ID · CNAM · Reverse Phone Lookup · Spam Detection · Do Not Call · Telephony · STIR/SHAKEN · MCP · Agent-Native · Compliance · Company

## Numbers Online on APIs.io

Everything profiled for Numbers Online is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/numbers-online/](https://apis.io/providers/numbers-online/)** — or go straight to one of the APIs or properties below.

### APIs (17)

- [Numbers Online MCP Server](https://apis.io/apis/numbers-online/numbers-online-mcp-server/) — A hosted, stateless, read-only Model Context Protocol server (JSON-RPC 2.0 over Streamable HTTP, protocol 2025-06-18) at POST…
- [Numbers Online A2A Agent](https://apis.io/apis/numbers-online/numbers-online-a2a-agent/) — An Agent-to-Agent (A2A protocolVersion 0.3.0, JSONRPC) endpoint at POST https://numbers.online/api/v1/a2a exposing four read-only skills — phone_lookup,…
- [Numbers Online Account API](https://apis.io/apis/numbers-online/numbers-online-account-api/) — Self-service API account: signup, balance, usage, credit top-ups, and the key lifecycle. Account-management endpoints require an account-level key with the…
- [Numbers Online Community reporting API](https://apis.io/apis/numbers-online/numbers-online-community-reporting-api/) — Key-gated spam/scam reporting — the give-to-get half of the community sensor (receipt-gated, tags-only, lane-scoped supplementary signals)
- [Numbers Online Inbound API](https://apis.io/apis/numbers-online/numbers-online-inbound-api/) — Inbound caller-intelligence lookup for operators, PBX, and softphones
- [Numbers Online Lookup API](https://apis.io/apis/numbers-online/numbers-online-lookup-api/) — Number lookup: line type, range carrier, CNAM, verstat, and a supplementary spam signal
- [Numbers Online MCP API](https://apis.io/apis/numbers-online/numbers-online-mcp-api/) — Model Context Protocol server for AI voice agents (Vapi, Retell, Pipecat, LiveKit): read-only phone-intelligence tools over Streamable HTTP
- [Numbers Online MSP API](https://apis.io/apis/numbers-online/numbers-online-msp-api/) — Multi-tenant control plane: per-tenant sub-keys, usage rollups, and suppression lists for MSPs and PBX resellers
- [Numbers Online Outbound API](https://apis.io/apis/numbers-online/numbers-online-outbound-api/) — Outbound pre-call checks (scrub + call-provenance) and number enrollment for spoofing-defense
- [Numbers Online Parsing API](https://apis.io/apis/numbers-online/numbers-online-parsing-api/) — Phone number parsing and validation endpoints
- [Numbers Online PBX API](https://apis.io/apis/numbers-online/numbers-online-pbx-api/) — Plain-text caller-id lookup for header-less PBX integrations (FreeSWITCH mod_cidlookup and similar)
- [Numbers Online Receipts API](https://apis.io/apis/numbers-online/numbers-online-receipts-api/) — Signed, privacy-safe lookup receipts (Ed25519) — verifiable "checked as of T" evidence
- [Numbers Online Reference API](https://apis.io/apis/numbers-online/numbers-online-reference-api/) — Reference data and examples
- [Numbers Online SBC / SIP API](https://apis.io/apis/numbers-online/numbers-online-sbc-sip-api/) — SIP redirect-server decisions for session border controllers (Kamailio, OpenSIPS, dSIPRouter, Sansay, Oracle/Acme Packet, ProSBC) via the operator-run shim…
- [Numbers Online System API](https://apis.io/apis/numbers-online/numbers-online-system-api/) — Operational endpoints (health checks)
- [Numbers Online Trust API](https://apis.io/apis/numbers-online/numbers-online-trust-api/) — Contact-suppression preference lookups
- [Numbers Online Webhooks API](https://apis.io/apis/numbers-online/numbers-online-webhooks-api/) — AI-voice-agent webhook adapters (Retell inbound, Vapi custom tool) over the same lookup backend

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [numbers-online-mcp.yml](https://apis.io/servers/numbers-online/numbers-online-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Numbers Online Agentic Access](https://apis.io/agentic-access/numbers-online/numbers-online-agentic-access/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Numbers Online Openapi Overlay](https://apis.io/overlays/numbers-online/numbers-online-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Numbers Online Authentication](https://apis.io/security/numbers-online/numbers-online-authentication/)
- [Numbers Online Domain Security](https://apis.io/security/numbers-online/numbers-online-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Numbers Online Plans Pricing](https://apis.io/plans/numbers-online/numbers-online-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Numbers Online Rate Limits](https://apis.io/rate-limits/numbers-online/numbers-online-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://numbers.online/)
- [Documentation](https://numbers.online/docs)
- [Getting started](https://numbers.online/developers)
- [API reference](https://numbers.online/docs)
- [Pricing](https://numbers.online/pricing)
- [Sign up](https://numbers.online/developers)
- [Support](https://numbers.online/concierge)
- [Changelog](https://numbers.online/api/spec)
- [Terms of service](https://numbers.online/terms)
- [Privacy policy](https://numbers.online/privacy)
- [GitHub](https://github.com/numbers-online)

## API Evangelist rating

**Kin Score 60.4** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 48.5 |
| Contract governance | 18.2 |
| Operational transparency | 60.5 |
| Developer ergonomics | 56.5 |
| Access clarity | 84.2 |

**Agent readiness 49.0** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | verified |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | verified |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 37.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/numbers-online/](https://apis.io/providers/numbers-online/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Numbers Online: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/numbers-online/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
