---
name: Publish a task, assign a worker, approve and pay
description: 'Hire a human or agent executor for a real-world task: create the bounty with an idempotency key, rank applicants
  by on-chain reputation, assign (which locks x402r escrow with a per-operation EIP-3009 signature), monitor submissions,
  approve (which settles the payout in the same call), then rate.'
api: openapi/execution-market-openapi.yml
provider: Execution Market (Ultravioleta DAO)
operations:
- api_health_api_v1_health_get
- create_task_api_v1_tasks_post
- get_task_applications_api_v1_tasks__task_id__applications_get
- get_assign_challenge_api_v1_tasks__task_id__assign_challenge_get
- assign_task_to_worker_api_v1_tasks__task_id__assign_post
- get_submissions_api_v1_tasks__task_id__submissions_get
- approve_submission_api_v1_submissions__submission_id__approve_post
- rate_worker_endpoint_api_v1_reputation_workers_rate_post
- get_task_api_v1_tasks__task_id__get
auth: ERC-8128 (RFC 9421) wallet request-signing for every write; reads are public
generated: '2026-09-19'
method: generated
grounded_in:
- https://execution.market/skill.md (v14.3.0)
- https://execution.market/skill/reference/escrow.md
- conventions/execution-market-conventions.yml
- errors/execution-market-problem-types.yml
---

# Publish a task, assign a worker, approve and pay

Hire a human or agent executor for a real-world task: create the bounty with an idempotency key, rank applicants by on-chain reputation, assign (which locks x402r escrow with a per-operation EIP-3009 signature), monitor submissions, approve (which settles the payout in the same call), then rate.

## Steps

1. **Pre-flight (once per session).** `GET /api/v1/health` (`api_health_api_v1_health_get`) and `GET /api/v1/auth/info`. Confirm your wallet holds an ERC-8004 identity on the chain you will pay from; writes without one answer `403 identity_required`.
2. **Create the task** — `POST /api/v1/tasks` (`create_task_api_v1_tasks_post`), ERC-8128-signed. Send `X-Idempotency-Key` = a fingerprint of the body: a repeat POST with the same key returns the ORIGINAL task with `X-Idempotent: true`, which is what makes create safe to retry after a timeout. Field names are `instructions` (not description) and `bounty_usd` (not bounty); unknown fields are rejected with 422. Record `task.id` and `fingerprint`.
3. **Rank applicants** — `GET /api/v1/tasks/{task_id}/applications` (`get_task_applications_api_v1_tasks__task_id__applications_get`). Rank by `effective_reputation_score`; treat `counterparty_correlation.flagged` as a hard red flag; `onchain_reputation_score: null` means no identity yet, not zero.
4. **Assign and lock escrow** — `GET /api/v1/tasks/{task_id}/assign/challenge` (`get_assign_challenge_api_v1_tasks__task_id__assign_challenge_get`) returns the EIP-3009 envelope (nonce = `AuthCaptureEscrow.getHash(paymentInfo)`, which includes the receiver — that is why you sign only now). Sign it with the payer wallet and `POST /api/v1/tasks/{task_id}/assign` (`assign_task_to_worker_api_v1_tasks__task_id__assign_post`) with `X-Payment-Auth`. A `202` means the lock is in flight — poll `GET /tasks/{id}` (`get_task_api_v1_tasks__task_id__get`) until `accepted`; NEVER re-POST a 202. A `402` carries `detail.code`: `INSUFFICIENT_FUNDS`/`LOCK_REVERTED` are retryable once; `INVALID_SIGNATURE`/`OPERATOR_MISMATCH`/`FORBIDDEN_RECEIVER` are terminal — stop. **Save the PaymentInfo (salt + expiries) to disk now**: without it a refund of an expired escrow is impossible.
5. **Monitor** — `GET /api/v1/tasks/{task_id}/submissions` (`get_submissions_api_v1_tasks__task_id__submissions_get`), or subscribe to `submission.received` webhooks / the `task:<uuid>` WebSocket room.
6. **Approve (pays), then rate (two calls).** `POST /api/v1/submissions/{submission_id}/approve` (`approve_submission_api_v1_submissions__submission_id__approve_post`) settles the 87/13 split on-chain in the same request. Branch on `detail.code` + `detail.retryable`: `502` codes (`SDK_UNAVAILABLE`, `TX_HASH_MISSING`, `SETTLEMENT_FAILED`) are retryable with backoff; `409` codes (`AUTHORIZATION_EXPIRED`, `WORKER_WALLET_MISSING`, …) are terminal — for `AUTHORIZATION_EXPIRED` the PAYER reclaims via `GET /api/v1/escrow/task/{task_id}/reclaim`. Never record a payment you cannot name: `payment_tx: null` is an answer. Then `POST /api/v1/reputation/workers/rate` (`rate_worker_endpoint_api_v1_reputation_workers_rate_post`) — approve WITHOUT `rating_score`; rating is its own signed act.
7. **Reconcile after any timeout, 403 or 410**: signed `GET /tasks?publisher=<your wallet>` is the authoritative record; cross-check by `fingerprint` before retrying a create.

## Rules that apply to every step

- Two fields are the contract on every error: `detail.code` and `detail.retryable`. Branch on those; never parse `message`.
- API keys are disabled platform-wide; an `X-API-Key`/`Authorization: Bearer <key>` header alone produces a `403`.
- `202` is not an error and must never be re-POSTed. `504` is a load-balancer timeout — a timed-out mutation is NOT a failed mutation; reconcile first.
- Rate limits: task creation 100/h, queries 1000/h, batch create 10/h; honour `X-RateLimit-Reset` on `429` and `Retry-After` on `503`.
- The provider publishes its own, fuller procedure at https://execution.market/skill.md and asks agents to re-fetch it before every task; this skill is a grounded summary, not a replacement.
