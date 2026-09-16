# Kit progress

> Maintained by the implementing AI. Tick tasks as they complete; record decisions the moment they're made. A fresh session resumes from this file alone.

## Scan results (Phase 0)

| Check | Finding |
|---|---|
| Consent to read the workspace layout and instructions file given? | _pending_ |
| Platform (files? shell? context-free sub-agent? persistent memory? context-usage number readable?) | _pending_ |
| A second model callable read-only from the shell? | _pending_ |
| Where the user's work lives (folder / vault / repo) | _pending_ |
| Existing standing-instructions file (path) | _pending_ |
| Existing project convention (do projects carry a STATUS or README?) | _pending_ |
| How the platform discovers skills (auto-loaded directory / rules-file reference / paste-only) | _pending_ |
| Existing skills Rome would call at step 6 (skill-structuring, pack-building, kit-export, voice) | _pending_ |
| A search index that needs refreshing after file moves? | _pending_ |

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
- [ ] Consent asked and given
- [ ] Platform + capabilities identified
- [ ] Workspace located (or chat-only path confirmed)
- [ ] Existing conventions and instructions file read
- [ ] Scan results recorded above

### Phase 1: Decisions
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
