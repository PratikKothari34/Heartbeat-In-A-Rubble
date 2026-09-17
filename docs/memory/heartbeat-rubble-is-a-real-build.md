---
name: heartbeat-rubble-is-a-real-build
description: Heartbeat In The Rubble is a real project the user intends to build, not a hackathon entry; the source doc is old reference material.
metadata:
  type: project
---

Heartbeat In The Rubble (drone-deployed MEMS seismic mesh for survivor detection) is a
project the user plans to actually build. `docs/reference/Heartbeat_In_The_Rubble.md` is
an OLD doc: its hackathon framing (Track T-01, pitch script, "questions judges will ask")
is stale context, not the goal.

As of 2026-09-17 there is no code. Repo scaffolded that day: `CLAUDE.md` (sole instruction
file), `docs/MASTER.md` (consolidated numbers, not an authority), `docs/decisions/` (ADRs,
only when actually required), `docs/memory/` (portable copy of this directory).

**Why:** The user corrected me on 2026-09-17 after I read the doc and framed the work as
hackathon prep.

**How to apply:** Treat it as engineering toward a buildable system — feasibility, BOM,
firmware, signal pipeline, TDoA solver. Never optimize for judges or demos. Precedence and
working rules live in `CLAUDE.md`; read it before acting.
