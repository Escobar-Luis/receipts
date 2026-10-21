---
title: "Product Brief: Receipts"
status: draft
created: 2026-10-21
updated: 2026-10-21
---

# Product Brief: Receipts

North-star deck: https://claude.ai/artifact/HQPtzmnoHGCX5zGmDjvRat

## Executive summary

Receipts checks the citations in an AI-written report before someone signs it. You upload or paste a report. An agent pulls out each claim and its citation, fetches the cited source with tool calls, finds the matching passage, and labels the claim supported, contradicted, not found or misquoted. Each label comes with a receipt: the exact source line, linked where the source allows it.

It is also Luis Escobar's portfolio project. It has to show four hiring teams (Unify, Quora, Provectus, Deloitte) five skills, on screen and not only in the code: an LLM in a deployed app, an agent with tool calls, retrieval with citations, evals, and a clear story. It runs entirely on free tiers, with no paid API key.

## The problem

Fluent AI text reads as true, and nobody checks the citations until after delivery. The person whose name is on the report pays for it:

- Deloitte refunded part of a ~A$440k Australian government report that held non-existent papers and a made-up quote from a federal judge; only 127 of its 141 references survived the correction ([TechRadar](https://www.techradar.com/pro/deloitte-forced-to-refund-aussie-government-after-admitting-it-used-ai-to-produce-error-strewn-report)).
- A ~C$1.6M, 526-page Newfoundland health plan cited at least 4 papers that don't exist, and the province ordered a full citation review ([HR Reporter](https://www.hrreporter.com/focus-areas/automation-ai/ai-errors-province-grapples-with-deloitte-report-marred-by-false-citations/393782)).
- Courts in 35 countries have issued about 1,600 decisions on AI-made content by mid-2026 ([MCE notice](https://www.notices.mce.ca.gov/2026/06/courts-cracking-down-on-error-strewn-ai-assisted-legal-briefs/)).
- At 11x, staff cited 70–80% churn among inbound customers, with hallucinations named as a reason ([TechCrunch](https://techcrunch.com/2025/03/24/a16z-and-benchmark-backed-11x-has-been-claiming-customers-it-doesnt-have)).

Today the check is manual and late: an academic, a judge or a client clicks the citations after the report ships.

## The solution

1. **Sign in.** One-click guest for anyone trying it; real sign-in saves your reports.
2. **Add a report.** Upload a file or paste text. Receipts counts the claims and citations it found.
3. **Check citations.** For each claim, the agent fetches the source (by URL, or by looking the reference up, e.g. Crossref), finds the closest passage with hybrid search (keyword plus meaning), and labels it.
4. **Read the receipts.** One row per claim: the label, the exact source line, a link to it, and the agent's steps.

Guardrails:
- A report with no citations gets a clear "nothing to check" message, not a guess.
- A source it can't read (paywalled, down) is marked unavailable and left for a human. It never guesses.

## How we'll know it works

Evals are the centre of the project, and they are visible: an evals page shows the latest scores after every deploy. The design follows *Practical LLM Evaluation for Production Systems*, chapter 1 (book consult, 2026-10-21):

- **Retrieval and label are scored separately**, as a 2x2: right passage or not, right label or not. "Right label, wrong passage" counts as luck, not success.
- **The labeling model is calibrated** against labels Luis sets by hand, cites the passage it used, and is versioned (model, prompt, rubric).
- **Tool calls get rule checks**: right URL or ID, a successful fetch, non-empty content. Failures and latency are tracked apart from quality.
- **Gates are tiered**: a bad citation passed as supported is a hard block; a drop in accuracy triggers a review decision.
- **Ground truth**: the original vs corrected Australian report (14 dropped references), plus planted errors (a fake DOI, a wrong author, a claim the source doesn't make). Planted cases extend the real core; they never replace it.
- **Model choice**: Receipts runs the same suite on each free model in the chain and recommends the best one.

## Who this serves

- **Users**: whoever signs a report an AI helped write: consultants and analysts. Success for them is catching a fake reference before the client does.
- **Audience**: hiring managers and engineers at the four target companies, who open a link for a few minutes. Success is that they see the agent work, see the evals, and understand both without reading code.

| Posting | What it asks for | Where Receipts shows it |
|---|---|---|
| Unify, Applied AI Engineer | evals from real tasks; traces; user visibility into agent actions | evals page, agent steps per claim |
| Quora, Full Stack New Grad | full stack with Python and React | React app, Python eval scripts |
| Provectus, Associate FDE | build the eval harness before the feature; explain to non-engineers | evals page, explainer page and clip |
| Deloitte, FDE AWS | GenAI on AWS; evals and monitoring; tests, CI/CD, logging | evals in CI, tracing; AWS mapping explained in the video |

## Scope

**In (first version):** guest and real sign-in; upload or paste; claim and citation extraction; source fetch by tool call; hybrid passage search; four labels with quoted source lines; the no-citations guardrail; the evals page; the explainer.

**Out:** AWS hosting (Cloudflare is free; the video explains the AWS mapping); paid models; checking claims that have no citation; writing or fixing reports.

## Constraints

- Everything free, no credit card, no paid API key. The template's stack (`STACK.md`): Cloudflare Workers, Neon, a free LLM chain with a daily cap and demo mode.
- A Worker request gets 10 ms of CPU, so heavy work runs at build time or in the browser.
- No brand logos; keep the "independent demo" footer; never invent facts.

## Open questions

1. What score counts as "worked"? Set it after the bootstrap shows how wide the interval is.
2. Is the original (uncorrected) Australian report still public to download?
3. Which free model labels best? The evals decide.
4. Which other public corrected reports could add real cases beyond the 14?
5. How many cases will Luis hand-label for calibration?
6. [ASSUMPTION] Link-to-line works for web pages; PDFs may only get a page link.
7. [ASSUMPTION] PDF text extraction runs in the browser, since the Worker's 10 ms CPU can't parse large PDFs.
8. Which free sign-in option fits the stack? (For John and Winston.)

## Vision

If it works, the same receipt check sits in front of any AI-written deliverable: reports, sales emails, answers. Same engine, different source types.
