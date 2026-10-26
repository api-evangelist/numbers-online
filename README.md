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

Numbers Online is a phone-number trust and intelligence service operated by Evergrow Management Pte. Ltd. (Singapore). It runs a free public reverse phone lookup with a community-driven, advisory spam-risk score, paid number verification for people and businesses, and a B2B API keyed on a single E.164 primitive: parsing and validation, single and batch lookup (line type, range carrier, CNAM, STIR/SHAKEN verstat and a low-confidence spam signal), signed inbound caller intelligence with Ed25519 receipts, an outbound pre-call do-not-contact scrub with call-provenance enrollment, consent-first list scrubbing, a ClearIP-compatible SBC/SIP redirect decision, a multi-tenant MSP control plane, and a hosted read-only MCP server plus Vapi/Retell webhooks for AI voice agents.

- Website: https://numbers.online/
- Developers: https://numbers.online/developers · API reference: https://numbers.online/docs · Pricing: https://numbers.online/pricing
- OpenAPI 3.0.3 (56 operations, provider-hosted source of truth): https://numbers.online/api/spec — harvested verbatim to `openapi/`
- llms.txt: https://numbers.online/llms.txt · A2A agent card: https://numbers.online/.well-known/agent-card.json · MCP server: `POST https://numbers.online/api/v1/mcp`
- GitHub: https://github.com/numbers-online

## What this profile holds (enrichment pass 2026-09-19)

| Artifact | Method | Notes |
|---|---|---|
| `openapi/` | searched | verbatim JSON original + YAML serialization |
| `a2a/` | probed | agent card graded **conformant**; endpoint answers 405/401 as declared |
| `mcp/` | probed | live `tools/list` (4 tools) + `initialize`; crosswalk to REST operationIds; official MCP registry listing |
| `well-known/` | probed | closed path list on apex + www with a negative control; only the agent card is served |
| `llms/` | searched | verbatim |
| `authentication/`, `agentic-access/`, `security/` | derived / generated / probed | pipeline scripts |
| `conventions/`, `errors/`, `lifecycle/`, `rate-limits/`, `plans/`, `changelog/`, `conformance/` | searched | from the spec description, docs, pricing and terms |
| `regulatory/` | searched | DSR process and report notice-and-action recorded; everything else checked and absent |
| `skills/`, `data-model/`, `overlays/`, `packages/` | generated / derived / searched | no SDKs exist on any registry — recorded honestly |

Not found (recorded, not fabricated): no security.txt, no OAuth/OIDC discovery, no RFC 9728 metadata, no api-catalog, no apis.json, no status page, no outbound webhooks or AsyncAPI, no SDKs, no CLI, no sandbox/test values, no WSDL or protobuf.
