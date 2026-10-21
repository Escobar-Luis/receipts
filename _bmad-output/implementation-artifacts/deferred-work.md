# Deferred work

## Deferred from: code review of PR #1, chore/bmad-setup (2026-10-21)

- **Two homes for planning docs.** BMad writes specs and stories to `_bmad-output/`; the template's `AGENTS.md` loop names `docs/spec.md` and `docs/memlog.md`. Deploy checks read neither, so nothing breaks today, but agents may write to both. Settle it in the brief/PRD stage and add one line to `AGENTS.md` saying which folder is the source of truth. Deferred: the fix edits agent-context files.
- **`AGENTS.md` doesn't mention BMad yet.** No note on the BMad version (bmad-toolbox 6.13.0-next) or the north-star deck link. Mary adds the deck link in stage 2. Deferred: the fix edits agent-context files.
