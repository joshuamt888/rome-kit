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
| DP-1 | Where a build's paper lives | _pending_ | |
| DP-2 | Who the second reviewer is | _pending_ | |
| DP-3 | Sub-agents or one thread | _pending_ | |
| DP-4 | Feedback loop depth | _pending_ | |
| DP-5 | How a long build survives a full chat | _pending_ | |
| DP-6 | Install location and name | _pending_ | |

## Tasks

### Phase 0: Environment scan
- [x] Consent asked and given
- [x] Platform + capabilities identified
- [x] Workspace located (or chat-only path confirmed)
- [x] Existing conventions and instructions file read
- [x] Scan results recorded above

### Phase 1: Decisions
- [ ] User oriented with `EXAMPLE-BUILD.md` before the first decision
- [ ] DP-1 through DP-6 decided and recorded above

### Phase 2: Install
- [ ] Protocol installed at the DP-6 location (path recorded here)
- [ ] `prompts.md` reviewer command adapted to DP-2 (or the paste note written)
- [ ] `SKILL.md` edits for DP-1 and DP-5 applied and listed here
- [ ] Agent definitions installed from `templates/agents/` (DP-3 A only)
- [ ] `runs.md` created, empty (DP-4 A or B)
- [ ] Builds home created (DP-1 B only)
- [ ] Wiring added to the standing-instructions file (file path recorded here)

| Install paths | |
|---|---|
| Protocol (`SKILL.md`) | _pending_ |
| Runs log | _pending_ |
| Agent definitions | _pending_ / n/a |
| Builds home | _pending_ / n/a |
| Instructions file edited | _pending_ |
| Edits made to `SKILL.md` / `prompts.md` | _pending_ |

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
