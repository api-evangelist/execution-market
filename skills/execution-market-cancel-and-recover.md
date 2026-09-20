---
name: Cancel a task and recover escrowed funds
description: 'Reverse a hire safely: cancel while the task is still published or accepted, and recover locked escrow after
  expiry through the payer-only on-chain reclaim path — with the windows the provider actually states.'
api: openapi/execution-market-openapi.yml
provider: Execution Market (Ultravioleta DAO)
operations:
- cancel_task_api_v1_tasks__task_id__cancel_post
- get_task_api_v1_tasks__task_id__get
- refund_to_agent_api_v1_escrow_refund_post
- get_task_reclaim_api_v1_escrow_task__task_id__reclaim_get
- list_tasks_api_v1_tasks_get
auth: ERC-8128 (RFC 9421) wallet request-signing for every write; reads are public
generated: '2026-09-19'
method: generated
grounded_in:
- https://execution.market/skill.md (v14.3.0)
- https://execution.market/skill/reference/escrow.md
- conventions/execution-market-conventions.yml
- errors/execution-market-problem-types.yml
---

# Cancel a task and recover escrowed funds

Reverse a hire safely: cancel while the task is still published or accepted, and recover locked escrow after expiry through the payer-only on-chain reclaim path — with the windows the provider actually states.

## Steps

1. **Check the window.** Cancel works only while the task is `published` or `accepted` (before evidence is submitted). Read the task signed: `GET /api/v1/tasks/{task_id}` (`get_task_api_v1_tasks__task_id__get`). Once evidence is in, cancel answers `409`.
2. **Cancel** — `POST /api/v1/tasks/{task_id}/cancel` (`cancel_task_api_v1_tasks__task_id__cancel_post`), ERC-8128-signed, body `{"reason": "..."}`. Confirm from the cancel response or a signed read: an UNSIGNED `GET /tasks/{id}` on a cancelled task returns `410 Gone` to non-participants — that is not a failed cancel.
3. **Escrow locked on a published/accepted task** — `POST /api/v1/escrow/refund` (`refund_to_agent_api_v1_escrow_refund_post`) returns the deposit to the payer.
4. **Expired task with locked escrow** — the cancel API answers `409 Cannot cancel task in 'expired' status`. Recovery is on-chain and payer-only: `GET /api/v1/escrow/task/{task_id}/reclaim` (`get_task_reclaim_api_v1_escrow_task__task_id__reclaim_get`) returns UNSIGNED calldata; the wallet that funded the escrow signs and sends it. It works precisely because `authorizationExpiry` has passed (`reclaim` is `onlySender(info.payer)`). You need the PaymentInfo saved at authorize time (salt, pre_approval_expiry, authorization_expiry, refund_expiry) — the server does not store the salt.
5. **Repricing is not an endpoint** — compose it: cancel the original, create a replacement at the new bounty preserving the remaining deadline, chain `replacement_of`, and reuse the same `X-Idempotency-Key` discipline so a timeout-retry cannot double it.
6. **Reconcile** — signed `GET /api/v1/tasks?publisher=<wallet>` (`list_tasks_api_v1_tasks_get`) lists every status and is the answer to "what actually happened".

## Rules that apply to every step

- Two fields are the contract on every error: `detail.code` and `detail.retryable`. Branch on those; never parse `message`.
- API keys are disabled platform-wide; an `X-API-Key`/`Authorization: Bearer <key>` header alone produces a `403`.
- `202` is not an error and must never be re-POSTed. `504` is a load-balancer timeout — a timed-out mutation is NOT a failed mutation; reconcile first.
- Rate limits: task creation 100/h, queries 1000/h, batch create 10/h; honour `X-RateLimit-Reset` on `429` and `Retry-After` on `503`.
- The provider publishes its own, fuller procedure at https://execution.market/skill.md and asks agents to re-fetch it before every task; this skill is a grounded summary, not a replacement.
