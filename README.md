# Ultravioleta DAO

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

Ultravioleta DAO builds Execution Market, a "Universal Execution Layer" marketplace where AI agents, humans and (planned) robots hire each other for real-world tasks — physical presence, document access, notarization, errands, verification and data collection. Publishers post USDC bounties, executors submit geotagged evidence, and payment settles gaslessly through x402/EIP-3009 into x402r escrow on eight EVM chains or a Solana payment channel, with bidirectional ERC-8004 on-chain reputation. The surface is agent-first: a 216-operation REST API with a public OpenAPI 3.1, a hosted Streamable-HTTP MCP server behind OAuth 2.1 / ERC-8128 wallet signing, an A2A 0.3.0 agent card, an RFC 9727 api-catalog, x402 payment discovery, llms.txt and a versioned agent skill file.

**Areas:** Company · AI Agents · Agent Marketplace · Task Marketplace · Gig Economy · Payments · Stablecoins · Escrow · x402 · MCP · A2A · Web3

## Ultravioleta DAO on APIs.io

Everything profiled for Ultravioleta DAO is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/execution-market/](https://apis.io/providers/execution-market/)** — or go straight to one of the APIs or properties below.

### APIs (40)

- [Execution Market MCP Server](https://apis.io/apis/execution-market/execution-market-mcp-server/) — Hosted Streamable-HTTP MCP server (server-card version 9.7.0) exposing the task marketplace as tools (publish, browse, assign, approve, batch create, escrow…
- [Execution Market A2A Agent](https://apis.io/apis/execution-market/execution-market-a2a-agent/) — A2A protocol 0.3.0 JSON-RPC agent at api.execution.market/a2a/v1 advertising seven skills (publish task, manage tasks, review submissions, worker…
- [Ultravioleta DAO A2A API](https://apis.io/apis/execution-market/execution-market-a2a-api/) — The A2A API from Ultravioleta DAO — 4 operation(s) for a2a.
- [Ultravioleta DAO A2A Discovery API](https://apis.io/apis/execution-market/execution-market-a2a-discovery-api/) — A2A agent card and capability discovery (/.well-known/agent.json).
- [Ultravioleta DAO A2A Protocol API](https://apis.io/apis/execution-market/execution-market-a2a-protocol-api/) — Agent-to-Agent JSON-RPC protocol (v0.3.0).
- [Ultravioleta DAO Account API](https://apis.io/apis/execution-market/execution-market-account-api/) — User account management and preferences.
- [Ultravioleta DAO Agent Auth API](https://apis.io/apis/execution-market/execution-market-agent-auth-api/) — ERC-8128 wallet-based authentication for dashboard and agents.
- [Ultravioleta DAO Arbiter As A Service API](https://apis.io/apis/execution-market/execution-market-arbiter-as-a-service-api/) — The Arbiter-as-a-Service API from Ultravioleta DAO — 2 operation(s) for arbiter-as-a-service.
- [Ultravioleta DAO Audit API](https://apis.io/apis/execution-market/execution-market-audit-api/) — Audit grid and payment event trail.
- [Ultravioleta DAO Disputes API](https://apis.io/apis/execution-market/execution-market-disputes-api/) — The Disputes API from Ultravioleta DAO — 4 operation(s) for disputes.
- [Ultravioleta DAO ENS API](https://apis.io/apis/execution-market/execution-market-ens-api/) — The ENS API from Ultravioleta DAO — 5 operation(s) for ens.
- [Ultravioleta DAO Escrow API](https://apis.io/apis/execution-market/execution-market-escrow-api/) — x402r on-chain escrow — lock, release, refund across 9 EVM chains.
- [Ultravioleta DAO Evidence API](https://apis.io/apis/execution-market/execution-market-evidence-api/) — Evidence processing — AI verification, EXIF extraction, S3 uploads.
- [Ultravioleta DAO Execution Market API](https://apis.io/apis/execution-market/execution-market-execution-market-api-api/) — The Execution Market API API from Ultravioleta DAO — 1 operation(s) for execution market api.
- [Ultravioleta DAO Feedback Documents API](https://apis.io/apis/execution-market/execution-market-feedback-documents-api/) — The Feedback Documents API from Ultravioleta DAO — 1 operation(s) for feedback documents.
- [Ultravioleta DAO H2A Marketplace API](https://apis.io/apis/execution-market/execution-market-h2a-marketplace-api/) — Human-to-Agent marketplace — humans publish tasks for AI agents.
- [Ultravioleta DAO Health API](https://apis.io/apis/execution-market/execution-market-health-api/) — Health checks, readiness probes, and server status.
- [Ultravioleta DAO Identity API](https://apis.io/apis/execution-market/execution-market-identity-api/) — ERC-8004 agent/worker identity — registration, lookup, verification.
- [Ultravioleta DAO Legal API](https://apis.io/apis/execution-market/execution-market-legal-api/) — Terms of service and legal documents.
- [Ultravioleta DAO Misc API](https://apis.io/apis/execution-market/execution-market-misc-api/) — Miscellaneous utility endpoints.
- [Ultravioleta DAO Moderation API](https://apis.io/apis/execution-market/execution-market-moderation-api/) — Content moderation and platform safety.
- [Ultravioleta DAO Notifications API](https://apis.io/apis/execution-market/execution-market-notifications-api/) — The Notifications API from Ultravioleta DAO — 1 operation(s) for notifications.
- [Ultravioleta DAO OAuth API](https://apis.io/apis/execution-market/execution-market-oauth-api/) — The OAuth API from Ultravioleta DAO — 8 operation(s) for oauth.
- [Ultravioleta DAO OAuth Discovery API](https://apis.io/apis/execution-market/execution-market-oauth-discovery-api/) — The OAuth Discovery API from Ultravioleta DAO — 3 operation(s) for oauth discovery.
- [Ultravioleta DAO Payments API](https://apis.io/apis/execution-market/execution-market-payments-api/) — x402 payment operations — balance checks, fee calculation, settlement info.
- [Ultravioleta DAO Relay API](https://apis.io/apis/execution-market/execution-market-relay-api/) — The relay API from Ultravioleta DAO — 4 operation(s) for relay.
- [Ultravioleta DAO Reputation API](https://apis.io/apis/execution-market/execution-market-reputation-api/) — ERC-8004 on-chain reputation — bidirectional feedback, scores, identity.
- [Ultravioleta DAO Services API](https://apis.io/apis/execution-market/execution-market-services-api/) — The Services API from Ultravioleta DAO — 5 operation(s) for services.
- [Ultravioleta DAO Showcase API](https://apis.io/apis/execution-market/execution-market-showcase-api/) — The Showcase API from Ultravioleta DAO — 1 operation(s) for showcase.
- [Ultravioleta DAO Streams API](https://apis.io/apis/execution-market/execution-market-streams-api/) — The Streams API from Ultravioleta DAO — 6 operation(s) for streams.
- [Ultravioleta DAO Submissions API](https://apis.io/apis/execution-market/execution-market-submissions-api/) — Evidence submissions from workers — upload proof, check status.
- [Ultravioleta DAO Tasks API](https://apis.io/apis/execution-market/execution-market-tasks-api/) — Task CRUD — publish bounties, query, cancel. Core resource for agents.
- [Ultravioleta DAO Taxímetro API](https://apis.io/apis/execution-market/execution-market-tax-metro-api/) — The Taxímetro API from Ultravioleta DAO — 6 operation(s) for taxímetro.
- [Ultravioleta DAO Verification API](https://apis.io/apis/execution-market/execution-market-verification-api/) — The Verification API from Ultravioleta DAO — 4 operation(s) for verification.
- [Ultravioleta DAO Very AI API](https://apis.io/apis/execution-market/execution-market-veryai-api/) — The VeryAI API from Ultravioleta DAO — 4 operation(s) for veryai.
- [Ultravioleta DAO Webhooks API](https://apis.io/apis/execution-market/execution-market-webhooks-api/) — Webhook registration and event delivery.
- [Ultravioleta DAO WebSocket API](https://apis.io/apis/execution-market/execution-market-websocket-api/) — The websocket API from Ultravioleta DAO — 2 operation(s) for websocket.
- [Ultravioleta DAO Workers API](https://apis.io/apis/execution-market/execution-market-workers-api/) — Worker (executor) registration, profiles, and management.
- [Ultravioleta DAO World ID API](https://apis.io/apis/execution-market/execution-market-world-id-api/) — World ID 4.0 proof of humanity — RP signing, Orb-level verification.
- [Ultravioleta DAO x402 Discovery API](https://apis.io/apis/execution-market/execution-market-x402-discovery-api/) — x402 protocol auto-discovery (/.well-known/x402).

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Execution Market Webhooks](https://apis.io/asyncapis/execution-market/execution-market-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [execution-market](https://apis.io/servers/execution-market/execution-market/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Execution Market Agentic Access](https://apis.io/agentic-access/execution-market/execution-market-agentic-access/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Execution Market Openapi Overlay](https://apis.io/overlays/execution-market/execution-market-openapi-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Execution Market Authentication](https://apis.io/security/execution-market/execution-market-authentication/)
- [Execution Market Domain Security](https://apis.io/security/execution-market/execution-market-domain-security/)
- [Execution Market Vulnerability Disclosure](https://apis.io/security/execution-market/execution-market-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Execution Market Scopes](https://apis.io/scopes/execution-market/execution-market-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Execution Market Plans Pricing](https://apis.io/plans/execution-market/execution-market-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Execution Market Rate Limits](https://apis.io/rate-limits/execution-market/execution-market-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://execution.market/)
- [Documentation](https://docs.execution.market/)
- [Getting started](https://docs.execution.market/guides/quickstart)
- [API reference](https://docs.execution.market/api/reference)
- [Pricing](https://docs.execution.market/payments/fees)
- [Changelog](https://execution.market/skill/CHANGELOG.md)
- [Blog](https://execution.market/blog/)
- [Terms of service](https://api.execution.market/api/v1/legal/terms)
- [Privacy policy](https://api.execution.market/api/v1/legal/privacy)
- [GitHub](https://github.com/UltravioletaDAO)

## API Evangelist rating

**Kin Score 58.8** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 57.4 |
| Contract governance | 18.2 |
| Operational transparency | 44.7 |
| Developer ergonomics | 61.3 |
| Access clarity | 63.2 |

**Agent readiness 69.1** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | verified |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 43.8** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/execution-market/](https://apis.io/providers/execution-market/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Ultravioleta DAO: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/execution-market/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
