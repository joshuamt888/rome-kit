# templates/: install matrix

What the installer (IMPLEMENT.md Phase 2) puts into the user's workspace, and which decision gates each.

| Template | Installed as | Gated by | Notes |
|---|---|---|---|
| `BUILD-STATUS.md` | `<skill install path>/templates/BUILD-STATUS.md` at install; then `<build folder>/STATUS.md` for a tier-3 build, or its Define, Plan and Run-card sections pasted into an existing STATUS for tier 2 | DP-1 (where a build's paper lives) | Copied at the start of every tier-2 or tier-3 build, then written over. Stubs, not content; the rules live in `skill/SKILL.md`. |
| `NEXT-CHAT.md` | `<skill install path>/templates/NEXT-CHAT.md` at install; then `<build folder>/NEXT-CHAT.md` at every retire of a tier-3 build | DP-1, DP-5 (how retiring works on your platform) | The hand-off. Five things: do-not list · read-first order · rules attributed · first action · model and mode line. |
| `runs.md` | `<skill install path>/references/runs.md` | DP-4 (the feedback loop) | Created once, empty, at install. The feedback loop appends one row per build; the review log gets one row per second-reviewer pass. |

None of these is installed blank into a build folder without the user knowing: the AI names the file in the gate line and the gate's approval is the ask (new files ask first).
