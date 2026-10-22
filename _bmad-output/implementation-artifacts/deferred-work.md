# Deferred work

## Deferred from: code review of PR #1, chore/bmad-setup (2026-10-21)

- [x] **Two homes for planning docs.** Resolved 2026-10-21 in https://github.com/Escobar-Luis/receipts/pull/2: Luis chose `_bmad-output/` as the source of truth; `AGENTS.md` now says so and its loop points there.
- [x] **`AGENTS.md` doesn't mention BMad yet.** Resolved 2026-10-21 in https://github.com/Escobar-Luis/receipts/pull/2: `AGENTS.md` names bmad-toolbox 6.13.0-next, `_bmad-output/` and the north-star deck link.

## Deferred from: code review of PR #4, book room findings (2026-10-22)

For Winston (architecture). Each one is a design decision the research note raises but doesn't settle:
- **Retries vs reruns vs replay.** The note accepts "last write wins" on a retry, but also asks for 3-5 reruns with variance and a replayable claim graph. Keep every attempt in the trace, and pick the shown result by an explicit rule.
- **Injection outcome.** "Caught an injection" says "label the claim" but names no label or status. Pick one (for example, "needs a human" plus a flag) and its ledger row (SG3/SG4).
- **"Needs a human" vs the four labels.** Does it replace a label or sit beside one? UI, metrics and evals must agree.
- **Confusion matrix scope.** It covers the four labels only; decide how "rate limited", "needs a human" and injection outcomes are scored.
- **EV3 status.** The ledger marks EV3 ✓, but the agent's own adversarial set (truncated passages, failed fetch, wrong page, loose paraphrase) is still missing. Reopen it as ~.
- **Open engine rows.** The orchestrator, embedding model, latency budget and cost (SD4, BE14, AW2, RG1/RG2, RG11, SG4, DA11). Check their ledger status first.
