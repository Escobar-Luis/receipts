---
title: "Receipts: checklist gap ledger"
created: 2026-10-21
updated: 2026-10-22
---

# Checklist gap ledger

One ledger for every BMad persona on Receipts (Luis, 2026-10-21). The items come from Luis's layer checklists, built from O'Reilly books and kept outside this repo; each line here is a short label, not the book's text.

**Rule.** Every persona reads this file before its stage, updates the status of the items it touches, and adds where each one landed. Only planning personas in a session with Luis change a status; build agents (including the GitHub Actions build) read it and leave statuses alone. Nothing gets dropped between stages: an item is covered, partly covered, missing, or skipped with a reason.

**Status:** ✓ covered · ~ partly · ✗ missing · – skipped (reason given)
**Owner** answers it: Mary (why), John (what must be true), Sally (how it feels), Winston (how it's built), Amelia (proof it works). John and Sally pair; Winston decides the how and explains it.
**Lands in:** brief, PRD, UX, arch (architecture doc), story.

PR16-PR19 added by the book room from Building AI-Powered Products, appendix (AI PRD template); the PRD says why an algorithm is needed, not which one.

Skipped layers: mobile (Receipts is web only), Claude Code (how Luis builds, not what the product does).

## Product requirements

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| PR1 | Problem in one sentence; why AI is needed | ✓ (PRD What it is) | Mary, John | brief, PRD |
| PR2 | One persona and what blocks them | ✓ (brief; PRD Who uses it) | Mary, John | brief, PRD |
| PR3 | A user story per feature | ✓ (PRD journeys) | John, Sally | PRD |
| PR4 | Who solves this already; what's different | ~ (prior art only) | Mary | brief |
| PR5 | North-star metric plus health metrics | ✓ (PRD M1-M5) | John | PRD |
| PR6 | Quality bar to launch | ~ (go/no-go; thresholds after bootstrap) | John | PRD |
| PR7 | Features ranked by value and effort | ✓ (PRD Features ranked) | John | PRD |
| PR8 | Build or buy per AI piece | ✓ (PRD data flow: buy models, build checker) | John, Winston | PRD, arch |
| PR9 | Assumptions, constraints, risks and fixes | ✓ (PRD Risks) | John | PRD |
| PR10 | Data available and legal to use | ✓ (PRD FR8, NFR4) | Mary, John | brief, PRD |
| PR11 | Rollout plan and go/no-go | ✓ (PRD Rollout) | John | PRD |
| PR12 | Watching accuracy after launch | ✓ (PRD M4) | John | PRD |
| PR13 | v1 vs later per pipeline part | ✓ (PRD Later list) | John | PRD |
| PR14 | Reviewer persona: what they see in five minutes | ✓ (brief; PRD UJ-1, F1) | Mary, John, Sally | brief, PRD, UX |
| PR15 | Agent/RAG success metrics (faithfulness, latency, cost) | ✓ (PRD M5, NFR1) | John | PRD |
| PR16 | AI MVP: model approach at a high level (off-the-shelf, hybrid or trained; data it needs) | ✓ (PRD model approach) | John, Winston | PRD |
| PR17 | High-level data flow only (client, server, where data goes); algorithms live in the architecture | ✓ (PRD data flow) | John | PRD |
| PR18 | Non-functional requirements: security, scale, speed, usability | ✓ (PRD NFR1-NFR6) | John | PRD |
| PR19 | Stakeholder and user update plan | ✓ (n/a: portfolio, PRD Rollout) | John | PRD |

## Evals

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| EV1 | Unit being judged (claim, report) | ✓ (PRD Labels: the claim) | John, Winston | PRD, arch |
| EV2 | Suites and slicing cases by type | ✓ (PRD M3 slices) | John | PRD |
| EV3 | Gold set plus adversarial set | ✓ (brief; PRD M3) | Mary | brief |
| EV4 | Synthetic cases only extend real ones | ✓ (brief; PRD M3) | Mary | brief |
| EV5 | Cheapest evaluator first (rules before judges) | ~ | Winston | arch |
| EV6 | Judge rubric, calibrated, cites evidence, versioned | ~ (brief "How we'll know"; PRD M3a calibration; rubric: arch) | Winston | arch |
| EV7 | How thresholds are set | ~ (bootstrap, M2) | John | PRD |
| EV8 | Block vs warn gates | ✓ (consult; warn-only for now) | John | PRD |
| EV9 | Online metrics after release | ✓ (PRD M4) | John | PRD |
| EV10 | Tool calls scored | ~ (brief; PRD M3a rule checks; how: arch) | Winston | arch |
| EV11 | Success = right final state, not one path | ✓ (PRD Labels) | John | PRD |
| EV12 | Recovery, loops, timeouts, step count | ✓ (PRD FR17-FR18) | John, Winston | PRD, arch |
| EV13 | Failure diagnosis order | ✗ (PRD Open items for Winston) | Winston | arch |
| EV14 | Retrieval and label scored separately | ✓ (brief; PRD M3) | John | PRD |
| EV15 | Evals in CI, stored and diffed | ~ (no diffs) | Amelia | story |

## LLM agents

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| AG1 | One agent or several | ~ (one, implied) | Winston | arch |
| AG2 | Each step worth its model cost | ✗ | Winston | arch |
| AG3 | User autonomy level | ✓ (PRD FR16) | John, Sally | PRD, UX |
| AG4 | Actions that need human approval | ✓ (PRD FR16: none) | John | PRD |
| AG5 | Narrow tools, strict schemas | ✗ | Winston | arch |
| AG6 | Local, API or MCP tools | ✗ | Winston | arch |
| AG7 | Tool choice: model, forced or pinned | ✗ | Winston | arch |
| AG8 | Invalid JSON, skipped tool, tool error | ✓ (PRD FR18) | John, Winston | PRD, arch |
| AG9 | Least privilege per tool | ✗ | Winston | arch |
| AG10 | ReAct, plan-then-execute or fixed chain | ✗ | Winston | arch |
| AG11 | Caps on steps and loops | ✓ (PRD FR17) | John, Winston | PRD, arch |
| AG12 | Context built per step | ✗ | Winston | arch |
| AG13 | Parallel tool calls | ✗ | Winston | arch |
| AG14 | Prompts versioned, changed with an eval run | ~ (brief: versioned; arch) | Winston | arch |
| AG15 | Every run traced and replayable | ~ (PRD FR3, FR3a; replay: Winston) | John, Winston | PRD, arch |

## Retrieval (RAG)

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| RG1 | Chunking method and size | ✗ | Winston | arch |
| RG2 | Embedding model | ✗ (none in stack) | Winston | arch |
| RG3 | Vector store and index | ~ (pgvector allowed) | Winston | arch |
| RG4 | Metadata per chunk | ✗ | Winston | arch |
| RG5 | Hybrid search and fusion | ~ (hybrid chosen) | Winston | arch |
| RG6 | Reranker | ✗ | Winston | arch |
| RG7 | Passages in prompt; model cites them | ~ | Winston | arch |
| RG8 | Hallucination check before trusting | ✓ (PRD FR2b) | John, Winston | PRD, arch |
| RG9 | Caches | ✗ | Winston | arch |
| RG10 | Re-embed changed sources | ✗ | Winston | arch |
| RG11 | Latency budget per stage | ~ (PRD NFR1; per stage: Winston) | John, Winston | PRD, arch |
| RG12 | Scale parts separately; lock-in cost | ✗ | Winston | arch |
| RG13 | Retrieval measured on a labeled set | ✓ (2x2) | John | PRD |
| RG14 | Per-document permissions | ✓ (PRD FR6) | John, Winston | PRD, arch |
| RG15 | Query rewriting and chat memory | – (no chat in v1) | John | PRD |

## Security and guardrails

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| SG1 | Trust boundaries and checks at each | ✗ | Winston | arch |
| SG2 | Fetched pages may hide instructions | ✓ (PRD FR2d) | John, Winston | PRD, arch |
| SG3 | Model output treated as untrusted | ~ (PRD FR2b, FR18; rest: arch) | Winston | arch |
| SG4 | Instructions and data separated in prompts | ✗ | Winston | arch |
| SG5 | Human approval for risky actions | – (no risky actions) | John | PRD |
| SG6 | Rate limits and injection detection | ~ (PRD FR2d, FR15; detection: arch) | Winston | arch |
| SG7 | Model and package provenance | ~ (pinned in STACK.md) | Winston | arch |
| SG8 | Tool code sandboxed | ✗ | Winston | arch |
| SG9 | Least-privilege DB role, per-user access | ~ (RLS pattern in db/rls.sql) | Winston | arch |
| SG10 | PII scrubbed; no leaked secrets | ✓ (PRD NFR4) | John, Winston | PRD, arch |
| SG11 | Every model and tool call logged | ~ (Langfuse) | Winston | arch |
| SG12 | GDPR consent, data minimization | ✓ (PRD FR8, FR14, NFR4) | John | PRD |
| SG13 | Secrets only in the Worker | ✓ (AGENTS.md rule) | Winston | arch |
| SG14 | Injection test set in CI | ~ (PRD FR2d, M3; CI: Amelia) | John, Amelia | PRD, story |
| SG15 | Per-user spend caps, max tool calls | ✓ (PRD FR15, FR17, NFR2) | John | PRD |

## Web frontend

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| FE1 | Speed and accessibility targets written down | ✓ (PRD NFR1, NFR3) | John, Sally | PRD, UX |
| FE2 | Document- or interaction-driven | ✗ | Sally, Winston | UX, arch |
| FE3 | What runs in the browser | ~ (PRD FR8: PDF to text in browser; rest: arch) | Winston | arch |
| FE4 | Persistent vs throwaway state | ✗ | Winston | arch |
| FE5 | Rendering per page | ~ (static SPA in stack) | Winston | arch |
| FE6 | Hydration strategy | – (SPA) | Winston | arch |
| FE7 | Slow data streams in | ✗ | Sally, Winston | UX, arch |
| FE8 | Cache rules per resource | ✗ | Winston | arch |
| FE9 | Safe retries, idempotency keys | ✗ | Winston | arch |
| FE10 | Where auth state lives; flaky networks | ✗ | Winston | arch |
| FE11 | SSE, WebSocket or NDJSON | ✗ | Winston | arch |
| FE12 | Agent progress, tool calls, citations shown live | ✓ (PRD F1: FR1-FR3) | John, Sally | PRD, UX |
| FE13 | Typed end to end | ~ (TypeScript, Zod) | Winston | arch |
| FE14 | Automated accessibility check | ✗ | Sally, Amelia | UX, story |
| FE15 | Loading, empty, error, slow-model states | ~ (PRD statuses, FR15; looks: Sally) | John, Sally | PRD, UX |

## Backend APIs

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| BE1 | API style per surface | ~ (REST via Hono) | Winston | arch |
| BE2 | Versioning | ✗ | Winston | arch |
| BE3 | Pagination | ✗ | Winston | arch |
| BE4 | Long runs: 202 plus a task id | ✓ (PRD FR10; how: Winston) | John, Winston | PRD, arch |
| BE5 | Idempotent endpoints | ✗ | Winston | arch |
| BE6 | Retry policy for outbound calls | ✗ | Winston | arch |
| BE7 | Rate limits per client and endpoint | ~ (per visitor) | Winston | arch |
| BE8 | Auth and validation on every endpoint | ~ (Zod) | Winston | arch |
| BE9 | Incoming webhooks verified | – (none planned) | Winston | arch |
| BE10 | Webhooks acked, retried, deduped | – (none planned) | Winston | arch |
| BE11 | Webhook payloads versioned | – (none planned) | Winston | arch |
| BE12 | One error schema | ✗ | Winston | arch |
| BE13 | Contract first (OpenAPI) | ✗ | Winston | arch |
| BE14 | Slow work queued, not inline | ✗ (10 ms CPU) | Winston | arch |
| BE15 | Timeouts, circuit breakers, correlation ids | ~ (LLM fall-through) | Winston | arch |

## DevOps and delivery

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| DV1 | Semantic versions; lockfile | ~ (lockfile, no tags) | Amelia | story |
| DV2 | Same artifact in every environment | ✓ (one Worker build) | Winston | arch |
| DV3 | Unit, integration, end-to-end split | ~ (vitest) | Winston, Amelia | arch, story |
| DV4 | Small branches; feature toggles | ✓ (one story, one branch) | Amelia | story |
| DV5 | CI on every PR; red blocks merge | ~ | Amelia | story |
| DV6 | Revert fast when main breaks | ✓ (merge log, revert command) | Amelia | story |
| DV7 | Blue-green, rolling or canary | ✗ | Winston | arch |
| DV8 | CI deploys with a machine identity | ~ (API token secret) | Winston | arch |
| DV9 | Who gets paged | – (portfolio demo) | John | PRD |
| DV10 | Bugs vs incidents; postmortems | – (portfolio demo) | John | PRD |
| DV11 | Rollback and fallback ready | ✓ (demo mode) | Winston | arch |
| DV12 | Agent-made changes reversible and logged | ✓ (PRs only) | Amelia | story |
| DV13 | Evals as a CI gate | ~ (promptfoo after deploy) | Amelia | story |
| DV14 | LLM calls mocked in unit tests | ✗ | Amelia | story |
| DV15 | Runbook for AI failures | ~ (PRD NFR2 demo mode) | John, Winston | PRD, arch |

## Observability

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| OB1 | Auto vs manual spans | ✗ | Winston | arch |
| OB2 | Trace context across services | ✗ | Winston | arch |
| OB3 | One wide event per run | ✗ | Winston | arch |
| OB4 | Stable span names | ✗ | Winston | arch |
| OB5 | Sampling; signal per need | ~ (Langfuse sampling) | Winston | arch |
| OB6 | SLIs per user journey | ✓ (PRD M4, NFR1) | John | PRD |
| OB7 | SLO window and burn-rate alerts | ✗ | Winston | arch |
| OB8 | LLM spans carry model, tokens, prompt version | ~ | Winston | arch |
| OB9 | Big or private prompts kept out of spans | ✓ (PRD NFR4) | John, Winston | PRD, arch |
| OB10 | Cost per request | ✓ (PRD M5) | John, Winston | PRD, arch |
| OB11 | Agent loop traced end to end | ~ (PRD F1 FR3 needs every tool call; how: Winston) | Winston | arch |
| OB12 | Thumbs and retries feed new eval cases | ✓ (PRD FR11a, FR3a) | John, Sally | PRD, UX |
| OB13 | Retrieval as its own span | ✗ | Winston | arch |
| OB14 | Backend chosen and its cost | ✓ (Langfuse Hobby) | Winston | arch |
| OB15 | One dashboard a reviewer can open | ✓ (PRD Evals, artboard 6) | John, Sally | PRD, UX |

## System design (by section)

| # | Section | Status | Owner | Lands in |
|---|---|---|---|---|
| SD1 | Requirements: functional, non-functional, constraints, golden-path demo, success metric | ✓ (PRD NFRs, M1) | John | PRD |
| SD2 | Estimation: workload, storage, token budget, embedding size | ~ (PRD NFR2; storage, embeddings: Winston) | John, Winston | PRD, arch |
| SD3 | API design: surfaces, endpoints, streaming | ✗ | Winston | arch |
| SD4 | Compute and agent: stateless first, loop, typed tools, memory, evaluator gates | ✗ | Winston | arch |
| SD5 | Data and storage: store per access pattern, consistency | ~ (Neon) | Winston | arch |
| SD6 | Caching, including LLM responses | ~ (AI Gateway option) | Winston | arch |
| SD7 | Async and queues; dead letters | ✗ | Winston | arch |
| SD8 | Scaling per tier | – (portfolio traffic) | Winston | arch |
| SD9 | Reliability: resume retries, fallback | ~ (LLM chain) | Winston | arch |
| SD10 | Security: auth, audit trail, injection | ✗ | Winston | arch |
| SD11 | Observability and evals | ~ | Winston | arch |
| SD12 | Deployment and cost per call | ~ | Winston | arch |

## Data

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| DA1 | Relational, document or graph per kind of data | ~ (Postgres) | Winston | arch |
| DA2 | Normalized vs copied | ✗ | Winston | arch |
| DA3 | Schema on write or read | ✗ | Winston | arch |
| DA4 | Read paths shape storage | ✗ | Winston | arch |
| DA5 | Encoding per boundary | ✗ | Winston | arch |
| DA6 | Old and new code read each other's data | ✗ | Winston | arch |
| DA7 | Field change rules | ✗ | Winston | arch |
| DA8 | Migrating old rows | ~ (db/init.sql) | Winston | arch |
| DA9 | ETL or ELT; batch or streaming | – (no pipelines) | Winston | arch |
| DA10 | Data quality checks per load | ✗ (eval set loads) | Winston | arch |
| DA11 | Insert, upsert or merge; deletes | ✗ | Winston | arch |
| DA12 | Task scheduling | – (no pipelines) | Winston | arch |
| DA13 | Where runs, chunks, embeddings and eval results live | ✗ | Winston | arch |
| DA14 | Re-runnable ingest; backfill | ✗ | Winston | arch |
| DA15 | Retention and PII policy | ✓ (PRD FR14: 14 days) | John | PRD |

## Cloud (AWS)

Receipts runs on Cloudflare, not AWS (brief). This layer is covered as a mapping: what each Cloudflare piece would be on AWS, explained in the video.

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| AW1 | Lambda, containers or EC2 per service | ✗ (map: Workers ≈ Lambda) | Winston | arch |
| AW2 | Jobs that outrun a time cap | ✗ (Worker: 10 ms CPU) | Winston | arch |
| AW3 | Cold starts | ✗ | Winston | arch |
| AW4 | What sets cost | ~ ($0 by rule) | Winston | arch |
| AW5 | Queues and fan-out | ✗ | Winston | arch |
| AW6 | Idempotent consumers; dead letters | ✗ | Winston | arch |
| AW7 | Pipeline orchestration | ✗ | Winston | arch |
| AW8 | Metrics, alarms, PII out of logs | ✗ | Winston | arch |
| AW9 | Least-privilege roles, no long-lived keys | ~ | Winston | arch |
| AW10 | Images versioned and scanned | – (no containers) | Winston | arch |
| AW11 | Deploy style and rollback speed | ✗ | Winston | arch |
| AW12 | Infrastructure as code | ~ (wrangler.jsonc, ship.yml) | Winston | arch |
| AW13 | Secrets in a manager, rotated | ~ (Worker secrets) | Winston | arch |
| AW14 | Budget alarm; one-command teardown | ✗ | Winston | arch |
| AW15 | Bedrock or direct model API | – (free chain) | Winston | arch |

## Customer communication

| # | Item | Status | Owner | Lands in |
|---|---|---|---|---|
| CC1 | Problem behind the ask | ✓ (brief) | Mary | brief |
| CC2 | What's true for the user after it ships | ✓ (PRD What it is) | Mary, John | brief, PRD |
| CC3 | Watched the real user do the task | ✗ (no user interviews) | Mary | brief |
| CC4 | Claims checked with more than one stakeholder | – (portfolio) | Mary | brief |
| CC5 | Written "done" a named role can verify | ✓ (PRD go/no-go) | John | PRD |
| CC6 | Out of scope and what's owed | ✓ (PRD Out of scope) | John | PRD |
| CC7 | Reviewer-level diagram; data-flow note | ~ (explainer planned) | Winston | arch |
| CC8 | Demo: time, audience, features confirmed | ✓ (PRD Rollout demo) | John, Sally | PRD, UX |
| CC9 | Demo rehearsed with a fallback | ~ (demo mode, recorded runs) | Amelia | story |
| CC10 | PoC champion, success criteria in writing | – (portfolio) | John | PRD |
| CC11 | Structured follow-up after meetings | – (portfolio) | John | PRD |
| CC12 | Say so when unsure | ✓ (never-invent rule) | all | AGENTS.md |
| CC13 | 2-minute demo plus one-page README | ~ (clip, README planned) | Amelia | story |
| CC14 | Decisions section shows trade-offs | ✗ | Winston | arch |
| CC15 | Explain at three levels: exec, user, engineer | ✓ (PRD F1) | John, Sally | PRD, UX |
