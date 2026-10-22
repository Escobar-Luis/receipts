---
title: "PRD: Receipts"
status: final
created: 2026-10-21
updated: 2026-10-22
---

# PRD: Receipts

Sections landed one at a time as Luis and John settled each gap in `_bmad-output/checklist-gaps.md`; after edge 5 Luis delegated the remaining calls to John, who settled them from the brief, `STACK.md` and the book room (each logged in `.memlog.md`). Sketches: the Receipts UI flow canvas (Claude Design).

## What it is

Receipts turns an evaluation method into a product. Teams that build AI search normally measure citation precision offline, on a test set: does each cited source really say what the answer claims? Receipts runs that same check live, on a report a person pastes in, and shows the receipt for every claim. The scope is the citation checker; the framing is "an eval method you can use". The first view is built for a normal person, not an engineer.

## Who uses it

- **Sam, a hiring reviewer**, opens the link cold and has about five minutes. Sam should see the agent work and the evals, and understand both without reading code. Most of Sam's time is at the glance and receipt levels.
- **Ana, an analyst** who signs a report an AI helped write, checks her own report before it goes to the client (UJ-2).
- **A power user** (an engineer reviewing the build, or someone checking a real report) wants to see how each label was reached: tool calls, timings, retrieval scores. They go to the full trace.
- **The project owner** (Luis) curates the sample report and the eval set.

Sam and Ana are illustrative personas drawn from the brief's users and audience, not interviewed people.

## Journeys

**UJ-1. Sam's five minutes (confirmed).** Sam opens the link cold and clicks "Try a sample report" without signing in. Claims fill in, paced as they ran (a recorded real run, NFR2). Sam opens a misquoted claim and sees the report's words beside the source line, with the agent's steps. Sam clicks Evals and sees the scores, then leaves knowing it works and that it's measured.

**UJ-2. Ana checks a real report (confirmed).** Ana, an analyst, has a client report due tomorrow that an AI helped draft. She signs in so the result is saved, uploads the PDF, and sees how many claims and citations Receipts found before anything runs. She starts the check, closes the tab, and comes back to a finished report. She filters to the problems, opens each receipt, fixes her report, and marks each claim reviewed. She downloads the list of receipts for her review note, then deletes the report.

## Feature: three levels of depth (F1)

One report view, three depths. Each deeper level is one deliberate step away, so a casual visitor sees things fill in and stay clickable, and the detail a power user wants never crowds the first view.

Checklist items behind it: FE12 (progress shown live), AG15 and OB11 (every run traced), OB15 (one page a reviewer opens), CC15 (explain at three levels), PR14 (the reviewer's five minutes).

- **FR1. Glance.** Each claim appears as one row that updates live as it moves through its states (waiting, fetching the source, finding the passage, checking the quote, done). A row shows only the claim, a status chip and, once done, its label or status (names as in "Labels and statuses"). Claims the agent can't check are rows too ("no citation", "unavailable"), never dropped.
- **FR2. Receipt.** One click or key press on a row opens its receipt: the report's words, the exact source line beside them, a link to that line (a page link where the source is a PDF), and a short plain-language list of the steps the agent took. Where the citation was resolved by a reference lookup, the receipt also shows the record found (title, authors, year, identifier). A claim with several citations shows one receipt per citation (up to 3; any more are listed as not checked), and the claim takes the worst verdict among them: contradicted, then misquoted, then not found, then supported.
- **FR2a. Show the mismatch.** On a "misquoted" or "contradicted" receipt, the words that differ between the report and the source line are highlighted, so the problem is visible in one look without reading both in full.
- **FR2b. The quote is checked, not trusted.** Before any label shows, a plain text check (not the AI model) confirms the quoted source line appears in the fetched source. A receipt that passes shows a small "verified in source" mark. When the line is not found, the receipt says so, the model's answer is retried once (FR18), and if the quote still isn't there the claim becomes "needs a human", never supported.
- **FR2c. Honest uncertainty.** Every label shows how strong its evidence is: strong or partial. Evidence too weak to call, or a case the agent cannot decide, makes the claim "needs a human" instead of being forced into a label, and it shows up in the default "needs review" view. How strength is judged is Winston's, checked by the evals.
- **FR2d. Caught an injection.** When a fetched source holds hidden instructions aimed at the checker, the agent does not follow them. The claim's receipt shows a plain note, "this source tried to instruct the checker", and the claim becomes "needs a human", never supported on that source. Pages like this are part of the eval set's tricky sources.
- **FR3. Full trace.** Inside the receipt (in the app; see NFR4 for what the external tracing tool keeps), a "Show full trace" control opens the detail: each tool call's input and output, time per step, the model and prompt version used, tokens and model calls for the claim, the passages retrieval considered with their scores, and the eval verdict where the case is in the eval set.
- **FR3a. Promote a trace to an eval case.** On the sample report and on the project owner's own reports, the project owner can save a claim from its full trace as a new eval case, with the label it should have had. The case is a copy kept in the eval set, so deleting the source report doesn't remove it; the project owner chooses this only for the sample and their own reports. Visitors' private reports never become eval cases. (Edge 8.)
- **FR4. Depth stays opt-in.** The glance level never shows tool inputs, scores, tokens or timings. Opening a deeper level is always the user's action, and the level they chose stays open while they move between claims in the same report.
- **FR5. Every level works by keyboard and screen reader**, including opening a receipt and the full trace.
- **FR6. Private reports stay private at every level.** The full trace of an uploaded or pasted report is visible only to the account that added it. Traces of the sample report are visible to everyone. Winston decides how.

Success signal: in a timed walkthrough, a first-time visitor reaches a receipt within 60 seconds of landing without help. (Also NFR1.)

## Feature: check a real report (F2)

From UJ-2. Checklist items behind it: PR3, BE4 (long runs), DA15 and SG12 (retention, data minimization), PR10 (data legal to use), SG15 (spend caps), FE15 (states).

- **FR7. Sign-in saves.** A signed-in user's reports are saved to their account. A guest can try the sample report without an account; checking their own report needs sign-in.
- **FR8. Add a report.** Upload a PDF or paste text. No Word files in v1. A PDF is turned into text in the browser; the file itself is never uploaded. The report text goes to the server once, so a model can pull out the claims and citations (as the brief's agent does), and is discarded after; only claims, citations and receipts are stored. Before the first upload, the user is told that claim text and source passages go to the free AI providers in the stack.
- **FR9. Counts before checking.** Before any check runs, the user sees how many claims and citations were found, and how many claims have no citation. A report with no citations gets the brief's plain "nothing to check" message and the check can't start.
- **FR10. The check outlives the tab.** A signed-in user can close the tab while a check runs and come back to the progress or the finished result.
- **FR11. Filter by label.** The default view is "needs review": every claim not labeled supported, including "needs a human".
- **FR11a. Flag a wrong label.** On a receipt, anyone can mark "this label looks wrong": any visitor on the sample report (once per browser), the account owner on their own reports. Flags are counted (M4); flags on the sample are reviewed by the project owner as candidate eval cases (FR3a).
- **FR12. Mark reviewed.** The user marks each claim reviewed and sees "n of n reviewed". On the sample, a guest's marks stay in their own browser.
- **FR13. Download the receipts.** One CSV file with every claim, its label or status, evidence strength, the source line and the link. Cells that could run as spreadsheet formulas are escaped, since source lines come from untrusted pages.
- **FR14. Delete means gone.** Deleting a report removes its claims, receipts and traces, and stops a check still running; nothing is written after. Every uploaded or pasted report's stored data is deleted automatically 14 days after it was added (the same 14-day window the stack uses to retire quiet Projects). v1 has no "keep forever".
- **FR15. Limits are visible.** A report over the size limit, a visitor over their rate limit, and a day over the free AI budget each get a plain message, never a silent failure or a guessed label. A v1 report holds up to 25 claims; a bigger one gets a clear "too big for the free demo" message, and nothing is checked. A claim stopped by a limit gets the status "rate limited", never "not found", and resumes when the limit allows. (Edge 9.)

## Labels and statuses

From brief open question 8. Checklist items behind it: EV1 (unit judged), EV11 (success is the right final state).

- **Labels** (the agent's verdict on a claim): supported, contradicted, misquoted, not found. "Not found" covers two cases, and the receipt says which: the cited work does not exist (the link answers "gone" after a retry, or a reference lookup finds no match), or the source is readable but holds no passage about the claim.
- **Statuses** (no verdict, left for a person): no citation, unavailable (the source exists but can't be read: paywall, blocked, network or server error), rate limited, needs a human (FR2b, FR2c, FR2d, FR17, FR18).
- **The unit judged is the claim.** A claim is right when it has the right label and, for supported, contradicted and misquoted, the right passage, by any path the agent took. Statuses are counted, never scored as right or wrong labels.

## How the agent behaves

Checklist items behind it: AG3, AG4 (autonomy, approvals), AG8 (bad output), AG11 and EV12 (caps, timeouts, recovery), SG15 (spend caps).

- **FR16. Read-only agent.** The agent only reads: it fetches sources and looks references up. Nothing it does needs a person's approval; the person starts the check and marks claims reviewed.
- **FR17. Caps per claim.** A claim gets at most 3 model calls (retries included), 8 tool calls and 60 seconds; time spent waiting as "rate limited" doesn't count toward the 60 seconds. A claim that hits a cap becomes "needs a human" with the reason, never a guessed label.
- **FR18. Recovery.** A failed fetch is retried once, then the claim is "unavailable". A model answer that can't be read is retried once, then the claim is "needs a human".

## Success metrics

Checklist items behind it: PR5 (north-star and health metrics), PR15 (faithfulness, latency, cost), EV7 (thresholds), EV8 (block vs warn gates), EV9 (online metrics), OB6 (SLIs), OB10 (cost per request).

- **M1. The one error that matters most: a wrong "supported".** A claim labeled supported when its source does not back it is the guardrail metric. It is counted on the eval set, weighted above every other mistake in the eval scores, and its count is shown on the Evals page Sam opens.
- **M2. It gates releases.** A wrong "supported" on the eval set blocks a release; a drop in other scores only asks for a review. Per the brief, the block stays warn-only until thresholds are set from a bootstrap run on the gold set; that run, with Luis's hand labels for calibration, is part of go/no-go, so the gate is hard at public launch. Amelia owns the bootstrap story.
- **M3. Quality scores** on the Evals page (the north-star: share of claims with the right label and, where one applies, the right passage): passage and label scored apart (the brief's 2x2), sliced by label, by source type (web page, PDF, reference lookup) and by case type (real, planted, injection, unavailable), with at least 5 cases per slice. Planted cases extend the real ones, never replace them. Target values are set from the bootstrap run, not guessed.
- **M3a. Model choice and tool calls.** The same suite runs on each free model in the chain and the Evals page recommends the best one (brief). Tool calls get rule checks (right URL or identifier, a successful fetch, non-empty content); their failures and latency are tracked apart from quality. The labeling model's agreement with Luis's hand labels is shown.
- **M4. After release** (online, from real use): share of claims ending "needs a human", rate-limited claims, "label looks wrong" flags, and time to first receipt.
- **M5. Cost per claim** (edge 10): model calls and tokens per claim, shown on the full trace and as an average on the Evals page, against the free daily budget.

## Non-functional requirements

Checklist items behind it: PR18, SD1, SD2, FE1, RG11, OB9, SG10, SG12, DA15, PR10. John drafted the numbers; Winston proves them or pushes back.

- **NFR1. Speed** (targets for Winston to prove). On the sample report, the first claim row is labeled within 15 seconds and a first-time visitor reaches a receipt within 60 seconds of landing. A 25-claim report finishes within 5 minutes; at about 3 model calls a claim against the 20-a-minute visitor limit, the limit alone takes close to 4 of those minutes, so Winston either fits it or proposes a different number.
- **NFR2. Budget.** About 3 model calls per claim (plus one or two per report to pull out the claims) against a shared 200-call daily cap means 2 to 3 full reports a day. So visitors never spend it: the sample report plays back a recorded real run, labeled with its date, and the project owner refreshes that recording. When the cap is reached, uploads wait for the next day with a plain message, and a check already running shows its remaining claims as "rate limited".
- **NFR3. Accessibility.** WCAG 2.2 AA, every level usable by keyboard and screen reader (FR5); labels never rely on colour alone.
- **NFR4. Privacy.** The uploaded file never leaves the browser; the report text is used once and discarded (FR8). Claims from uploaded or pasted reports are visible only to their account (FR6) and deleted after 14 days (FR14). Claim text and source passages do go to the free AI providers in `STACK.md`, which excludes providers that train on prompts, and the user is told so (FR8). The external tracing tool keeps timings, counts and labels for private reports, not claim or source text; today `llm()` sends full inputs and outputs to it, so Winston adds redaction there. Sample-report traces are complete.
- **NFR5. Security.** Every fetched page is untrusted input (FR2d). The checker fetches only public web addresses (never private or internal ones), with size and time limits, and only text, web pages and PDFs, so it can't be used as a proxy. Keys and the database live only on the server.
- **NFR6. Scale.** Built for demo traffic, inside the free tiers in `STACK.md`: 20 model calls a minute per visitor, 200 a day in total.

## High-level data flow

Checklist items behind it: PR16 (model approach), PR17 (data flow), PR8 (build or buy). Algorithms are Winston's.

1. The browser turns the report into text; the server has a model pull out claims and citations, then drops the text.
2. The server checks each claim: fetch the source, find the passage, ask a model for the label, check the quote in plain code (FR2b), save the receipt.
3. The browser shows progress and receipts as they land, and can be closed (FR10).

Model approach: off-the-shelf free models through the project's one model gateway (`llm()`), no training. The product is the hybrid: models propose, plain code checks the quote, evals measure both. Data it needs: the public corrected report and, if still public, its original (brief open question 2), planted cases, and labels Luis sets by hand (brief).

## Features ranked

Checklist item behind it: PR7 (value and effort), PR13 (v1 vs later). Value is what Sam sees in five minutes.

1. Sample report checked live, three levels of depth (F1, FR2a, FR2b).
2. Evals page with the wrong-"supported" count (M1 to M3).
3. Honest uncertainty and the caught injection (FR2c, FR2d).
4. Sign-in, upload, a check that outlives the tab (F2).
5. Filters, mark reviewed, download, flags (FR11 to FR13, FR11a).
6. Promote a trace to an eval case (FR3a).

Later, not v1: Word files, checking claims with no citation, keeping reports past 14 days, other source types (images, tables).

## Risks

Checklist item behind it: PR9.

| Risk | What we do |
| --- | --- |
| The free model budget runs out during a demo | Sample replays a recorded run, labeled (NFR2) |
| Sources block fetching (paywalls, bot walls) | "Unavailable" status, never a guess |
| PDF text comes out garbled | Counts shown before checking (FR9), so the user sees it early |
| Reviewer visits use up the free budget | The sample plays a recorded run (NFR2) |
| A page tries to steer the checker | FR2d, plus injection pages in the eval set |
| The model labels wrongly | Plain-code quote check (FR2b), M1 gate, "needs a human" |
| Someone uploads a confidential report | File stays in the browser, text discarded after extraction, owner-only, 14-day delete, provider notice (FR8, NFR4) |

## Rollout and go/no-go

Checklist items behind it: PR11, CC5, CC8, PR19.

- **Go** when: the bootstrap run has set thresholds and the eval run shows no wrong "supported" on the gold set (M2), NFR1 holds on the sample, and someone not on the build reaches a receipt and the Evals page in a timed walkthrough without help.
- **Rollout:** deploy through the template's ship workflow, then share the link. The five-minute demo: the sample report, one misquoted receipt, one caught injection, the Evals page.
- **Updates:** a portfolio project has no stakeholders to brief; the README, the explainer page and the how-it-works clip carry the story.

## Out of scope

Writing or fixing reports, paid models or tiers, AWS hosting (the clip explains the mapping), and the brief's "Out" list.

## Open items for Winston

- How a receipt and the full trace look and animate: the UI recon (`research/recon-ui-animation-2026-10-21.md`) suggests patterns; Winston picks the tools.
- Whether stored traces link out to the tracing tool or render only in the app (FR6, NFR4).
- What drives a check that outlives the tab on the free tier (FR10); whether Queues, Durable Objects or Workflows are free is unverified.
- Free sign-in option (brief question 6), embeddings for the meaning half of hybrid search (brief question 11), and how strict the quote match is (FR2b).
- Whether NFR1's numbers hold; push back with measurements if not.
- The Workers Free limit on outbound requests per invocation (FR17 allows up to 11 calls per claim), next to FR10's driver.
- Redaction of claim and source text in `llm()` tracing for private reports (NFR4), and safe fetching (NFR5).
- A replayable state machine per claim, so any run can replay and the full trace is its graph (book room edge 7).
- Failure diagnosis order (brief question 7, ledger EV13).
- The Python eval scripts' `stack_note` in the README, and how eval model calls go through `llm()` (brief question 9).
- Motion and AutoAnimate from the UI recon are additions to `STACK.md`: pin them if adopted.

Book room edges: 1 to 5 are FR2a to FR2d and M1/M2; 6 (an eval method as the product) is "What it is"; 7 is above; 8 is FR3a; 9 is in FR15; 10 is M5.
