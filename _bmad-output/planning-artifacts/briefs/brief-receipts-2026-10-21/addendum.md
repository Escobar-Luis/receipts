---
title: "Receipts brief: addendum"
created: 2026-10-21
updated: 2026-10-21
---

# Addendum: depth for the PRD and architecture

## Posting sources

- Unify, Applied AI Engineer: https://www.linkedin.com/jobs/view/4482028342 (saved: `~/dev/ai-engineering-journey/apply/postings/4482028342.txt`)
- Quora, Full Stack New Grad: no link saved (`apply/postings/5494e6a1-a973-46af-b9f3-57208eb91b52.txt`)
- Provectus, Associate FDE: no link saved (`apply/postings/bi-11787559.txt`)
- Deloitte, FDE AWS: https://apply.deloitte.com/en_US/careers/InviteToApply?jobId=350570 (the saved file is a summary, not the full posting: `apply/postings/4418120330.txt`)

## Party-mode findings (2026-10-21)

Gaps found against the five skills: no AWS (Deloitte), no Python (Quora), evals nobody can see, agent steps hidden. Luis chose: visible evals first; Python for evals; Cloudflare over AWS, explained in the video; guest plus real sign-in.

UI sketches discussed (not designs yet):
- Evals page: score cards (recall, precision, quotes verified, best free model), the 2x2, missed cases with the agent's steps.
- Flow: sign in → add report → results per claim → no-citations guardrail.

## Evals checklist gap check (`~/dev/ai-engineering-journey/docs/checklists/evals.md`)

- Covered: gold set; adversarial set.
- Partly: small real core (14); quote-exists check is a rule; traces exist but aren't shown; CI runs evals without diffs; unit judged undecided.
- Missing at brief time: slicing cases by type; judge calibration; thresholds; block vs warn gates; tool-call scoring; timeouts, loops, recovery; failure diagnosis order; retrieval vs label scored separately. The consult answered calibration, thresholds, gates, tool calls and the retrieval/label split; slicing, timeouts and diagnosis order are still open for the PRD.

## Book consult

Record: `~/dev/ai-engineering-journey/research/2026-10-21-consult-receipts-evals.md`. Live map: https://claude.ai/artifact/TK7XvbCaho2i1Sj3hDqAs3. Decisions go into the architecture doc when Winston creates it.

## Prior art for scoring

CiteAudit (https://arxiv.org/abs/2602.23452); CiteCheck (https://www.alphaxiv.org/abs/2605.27700), 88.7 macro-F1 on 982 physics citations.
