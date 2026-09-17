# Kit progress

> Maintained by the implementing AI. Tick tasks as they complete; record decisions the moment they're made. A fresh session resumes from this file alone.

## Scan results (Phase 0)

| Check | Finding |
|---|---|
| Consent to read the workspace layout and instructions file given? | Yes, 2026-09-17, Josh: "get it on both devices but lets also start with step one" |
| Platform (files? shell? context-free sub-agent? persistent memory? context-usage number readable?) | Claude Code (Fable 5.1) on two Macs: MacBook Air (Josh) and Mac mini (Jarvis, agents, reachable by SSH from the Air). Files yes · shell yes · fresh-context sub-agents yes (Agent tool, per-agent model + effort) · persistent memory yes (auto-memory + claude-mem) · context number: a remaining-token counter is visible in-session, not a percent-of-window from a file |
| A second model callable read-only from the shell (own / shuttled through the user / none)? | None confirmed. No codex/gemini/opencode/ollama on PATH. `aider` is installed (Python 3.9 user bin) but its model and API key are unverified. Fallback: fresh Claude sub-agent (DP-2 B) |
| Where the user's work lives (folder / vault / repo) | Obsidian vault `~/steady-brain` on both Macs (Obsidian Sync). Code in `~/repos` on each machine, not synced. Never `~/Documents` (iCloud) |
| Existing standing-instructions file (path) | `~/steady-brain/CLAUDE.md` (a router, one route line per topic; rule 8: new knowledge goes in a depth file). No `~/.claude/CLAUDE.md` |
| Existing project convention (do projects carry a STATUS or README?) | Yes, strict: `projects/<name>/` with README (identity), STATUS (state only), History/LOG, History/LESSONS, NEXT-CHAT (on retire). 16 projects, all carry both. Template in `projects/(PROJECT TEMPLATE)`. Tasks tagged #ai/#assist/#decide/#manual/#call. A Stop hook (retire-gate) blocks a session that edited STATUS without a LOG entry |
| How the platform discovers skills (auto-loaded directory / rules-file reference / paste-only) | Auto-loaded from `~/.claude/skills/` on both Macs. Vault folder skills (`skills/shared/<name>/SKILL.md`) are symlinked there on both machines; the symlink itself does not sync (tripwire 3) |
| Existing skills Rome would call at step 6 (skill-structuring, pack-building, kit-export, voice) | skill-creation (skill structuring) · build-expertise (knowledge packs) · terraform (kit export) · josh-voice (`skills/shared/josh-voice.md`, anything sent in Josh's name). Also installed and overlapping on the "let's build" trigger: superpowers brainstorming / writing-plans / executing-plans / verification-before-completion, and ponytail (minimal-code discipline) |
| A search index that needs refreshing after file moves? | Yes, qmd over the vault. Nightly LaunchAgent at 2am runs `qmd update && qmd embed && qmd cleanup`; run the same by hand after a build moves files |

## Decisions (Phase 1)

| # | Decision | Choice | Notes |
|---|---|---|---|
| DP-1 | Where a build's paper lives | **A**, the vault's project convention | Tier 3 = `projects/<slug>/` with the standard file set (README, STATUS, History/, NEXT-CHAT); tier 2 = Define + plan in the STATUS of the project it changes; tier 1 = runs-log row only. Catch-all for a small build no project owns: `projects/_builds/STATUS.md`. Decided 2026-09-17 |
| DP-2 | Who the second reviewer is | **B**, a fresh Claude sub-agent | No second vendor CLI on either Mac. `checker` agent, strongest model, high effort, gets only the locked goal, done list and plan. Gate lines always say what ran. Switch to A = one block edit in `prompts.md` if a Codex/Gemini CLI is ever installed. Decided 2026-09-17 |
| DP-3 | Sub-agents or one thread | **A**, four named sub-agents | `researcher`, `builder`, `grep-reader` on a mid-cost model (Sonnet 5; medium/medium/low effort), `checker` on the strongest (Fable 5.1, high). Installed to `~/.claude/agents/` on BOTH Macs (outside the vault, tripwire 3). Fan-out capped per plan; never more fixture agents than test cases; cheapest tier never without Josh's permission. Decided 2026-09-17 |
| DP-4 | Feedback loop depth | **A**, loop on, default 3 | Runs log at `<skill>/references/runs.md`; row + rule re-read + day-later fresh read. Josh can answer 1 at any close line. Decided 2026-09-17 |
| DP-5 | How a long build survives a full chat | **B**, retire by structure | No percent-of-window number is readable in Claude Code (only a remaining-token budget). SKILL.md § 3 percentage ladder replaced with: retire at every hand-off point the plan names, never more than two steps past step 5 in one chat. Hand-off file = the project's `NEXT-CHAT.md` (existing convention). Decided 2026-09-17 |
| DP-6 | Install location and name | **A+B**, vault skill + symlink; name **Rome**; trigger **narrow** | Skill at `~/steady-brain/skills/shared/rome/` (SKILL.md, references/, templates/), synced by Obsidian; symlinked to `~/.claude/skills/rome` on BOTH Macs. Triggers: "Rome", "build mode", "/rome", "step back on X", mid-flight re-entry. NOT "let's build X" (superpowers brainstorming/writing-plans keep it). No name collision in the vault. Decided 2026-09-17 |

## Tasks

### Phase 0: Environment scan
- [x] Consent asked and given
- [x] Platform + capabilities identified
- [x] Workspace located (or chat-only path confirmed)
- [x] Existing conventions and instructions file read
- [x] Scan results recorded above

### Phase 1: Decisions
- [x] User oriented with `EXAMPLE-BUILD.md` before the first decision
- [x] DP-1 through DP-6 decided and recorded above

### Phase 2: Install
- [x] Protocol installed at the DP-6 location (path recorded here)
- [x] `prompts.md` reviewer command adapted to DP-2 (or the paste note written)
- [x] `SKILL.md` edits for DP-1 and DP-5 applied and listed here
- [x] Agent definitions installed from `templates/agents/` (DP-3 A only)
- [x] `runs.md` created, empty (DP-4 A or B)
- [x] Builds home created (DP-1 B only) — n/a under A; catch-all `projects/_builds/` created instead
- [x] Wiring added to the standing-instructions file (file path recorded here)

| Install paths | |
|---|---|
| Protocol (`SKILL.md`) | `~/steady-brain/skills/shared/rome/SKILL.md` (vault, Obsidian-synced) + symlink `~/.claude/skills/rome` on the Air and the mini |
| Runs log | `~/steady-brain/skills/shared/rome/references/runs.md` |
| Agent definitions | `~/.claude/agents/{researcher,builder,grep-reader}.md` model `sonnet` (effort medium/medium/low), `checker.md` model `fable` effort high; on BOTH Macs |
| Builds home | n/a (DP-1 A). Catch-all `~/steady-brain/projects/_builds/STATUS.md` + `History/LOG.md` (retire-gate hook requires the LOG) |
| Instructions file edited | `~/steady-brain/CLAUDE.md`, one route-table row after "Starting a new project"; also one line in `skills/README.md` |
| Edits made to `SKILL.md` / `prompts.md` | SKILL.md: vault seven-field frontmatter added; description narrowed (no "let's build X"); § 1 catch-all → `projects/_builds/STATUS.md` + note that tier 3 uses the vault project convention; § 3 percentage ladder → retire-by-structure sentence; orchestrator line names the four agents. prompts.md: codex command block → "dispatch `checker`" note. templates/BUILD-STATUS.md: frontmatter → vault fields. research.md, NEXT-CHAT.md, runs.md unchanged |

### Phase 3: First live run
- [ ] Build chosen with the user (small, real); tier and mode stated
- [ ] Steps 1 to 8 run, every gate passed by the user's word
- [ ] Verification test 1: fresh session, user's own words, protocol fired without being named
- [ ] Verification test 2: fresh session states step, locked goal and next action from the paper alone
- [ ] First `runs.md` row appended

| First build | |
|---|---|
| What it was + tier | _pending_ |
| Where its paper lives | _pending_ |
| Trigger sentence used, and did it fire? | _pending_ |
| Cold-read answer (one line) | _pending_ |
| Elapsed minutes, install / first build | _pending_ |

### Phase 4: Wrap
- [ ] User walked through what's installed and where
- [ ] Install record copied to `<skill install path>/references/install-record.md`
- [ ] This file fully ticked; final state recorded

## Blockers

- none
