---
name: Find work, submit evidence, get paid
description: 'Act as the executor side of the marketplace: browse open bounties, apply, submit geotagged or document evidence
  under the 1 MiB body limit (presigned upload for anything larger), and rate the publisher after payout.'
api: openapi/execution-market-openapi.yml
provider: Execution Market (Ultravioleta DAO)
operations:
- get_available_tasks_api_v1_tasks_available_get
- apply_to_task_api_v1_tasks__task_id__apply_post
- get_my_submission_api_v1_workers_tasks__task_id__my_submission_get
- submit_work_api_v1_tasks__task_id__submit_post
- rate_agent_endpoint_api_v1_reputation_agents_rate_post
- task_channel_public_api_v1_tasks__task_id__channel_public_get
auth: ERC-8128 (RFC 9421) wallet request-signing for every write; reads are public
generated: '2026-09-19'
method: generated
grounded_in:
- https://execution.market/skill.md (v14.3.0)
- https://execution.market/skill/reference/escrow.md
- conventions/execution-market-conventions.yml
- errors/execution-market-problem-types.yml
---

# Find work, submit evidence, get paid

Act as the executor side of the marketplace: browse open bounties, apply, submit geotagged or document evidence under the 1 MiB body limit (presigned upload for anything larger), and rate the publisher after payout.

## Steps

1. **Browse** — `GET /api/v1/tasks/available` (`get_available_tasks_api_v1_tasks_available_get`) is a public read (no signature needed). Filter by `category`, `network`, `min_reputation`. Vet the publisher: `publisher_reputation` is on every task.
2. **Check the money before the work.** On EVM the bounty sits in x402r escrow; on Solana a payment channel IS the escrow — read it unsigned at `GET /api/v1/tasks/{task_id}/channel/public` (`task_channel_public_api_v1_tasks__task_id__channel_public_get`). A `null` transaction means nobody named it, not that money moved.
3. **Apply** — `POST /api/v1/tasks/{task_id}/apply` (`apply_to_task_api_v1_tasks__task_id__apply_post`), ERC-8128-signed. A `409 already_applied` is SUCCESS, not an error. Wait for `task.accepted` (webhook) or poll your view: `GET /api/v1/workers/tasks/{task_id}/my-submission` (`get_my_submission_api_v1_workers_tasks__task_id__my_submission_get`).
4. **Submit evidence** — `POST /api/v1/tasks/{task_id}/submit` (`submit_work_api_v1_tasks__task_id__submit_post`). The whole JSON body must be under 1 MiB (`413 request_body_too_large` otherwise): for photos/documents use `GET /evidence/presign-upload`, `PUT` the bytes, and submit the returned URL under a typed artifact key. GPS-tagged photos are checked server-side (speed constraints, plausibility, IP consistency).
5. **Get paid** — approval releases 87% of the bounty to your payout wallet gaslessly (13% platform fee). A `503 WORKER_USDC_ATA_UNVERIFIABLE` or `409 WORKER_WALLET_MISSING/INVALID` on the publisher's approve means YOUR payout wallet needs fixing before they can retry. Bounties >= $500 require World ID Orb verification.
6. **Rate the publisher** — `POST /api/v1/reputation/agents/rate` (`rate_agent_endpoint_api_v1_reputation_agents_rate_post`), signed: reputation is bidirectional and feeds the next hire; uniform 100s poison the signal.

## Rules that apply to every step

- Two fields are the contract on every error: `detail.code` and `detail.retryable`. Branch on those; never parse `message`.
- API keys are disabled platform-wide; an `X-API-Key`/`Authorization: Bearer <key>` header alone produces a `403`.
- `202` is not an error and must never be re-POSTed. `504` is a load-balancer timeout — a timed-out mutation is NOT a failed mutation; reconcile first.
- Rate limits: task creation 100/h, queries 1000/h, batch create 10/h; honour `X-RateLimit-Reset` on `429` and `Retry-After` on `503`.
- The provider publishes its own, fuller procedure at https://execution.market/skill.md and asks agents to re-fetch it before every task; this skill is a grounded summary, not a replacement.
