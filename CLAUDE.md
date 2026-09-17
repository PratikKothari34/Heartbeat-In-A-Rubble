# CLAUDE.md

**Project:** Heartbeat In The Rubble — drone-deployed MEMS seismic mesh for survivor detection.
**Status:** pre-code. Only artifact is the old reference doc (`docs/reference/`), whose hackathon framing is stale.

## Response rules

- Technical language, plain-English gloss alongside. No overexplaining.
- No filler. To the point. Bullets preferred.
- Elaborate only when asked.
- Something feels wrong → check the output twice, then ask.
- Raise a concern once, then execute. Don't re-litigate.
- When a rebuild or the complex solution is the right one, use it. Never recommend a cheap option that isn't the best.
- Optimization is key.

## Git

- Run `git commit` and `git push` directly. No permission needed.
- No `Co-Authored-By` trailer.
- No absolute system paths in commit messages.
- Rewriting pushed history (rebase, amend, force-push) needs explicit go-ahead first.

## Source of truth

Precedence, highest first:

1. **`CLAUDE.md`** — this file. The only project instruction file. No local, private, or nested variant.
2. **`docs/decisions/`** — ADRs. Binding on any decision they cover.
3. Anything below this line only if absolutely required.

- **`docs/MASTER.md`** — consolidated read, not an authority. Loses to decisions, wins on numbers.
- Every decision reflects into the docs. A later doc edit can overwrite an earlier one — the doc is live, not an archive.
- Write an ADR **only when actually required**: irreversible, cross-cutting, or contested. Routine choices are not logged.

## Memory

- **`docs/memory/`** — portable copy. Travels with this folder.
- Original is path-keyed at `~/.claude/projects/<workspace-slug>/memory/`. Renaming or moving this workspace orphans it; `docs/memory/` is the recovery copy.
- After any memory write, mirror path-keyed → `docs/memory/`. Both must agree.
