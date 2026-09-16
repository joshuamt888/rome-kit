# IMPLEMENT: install walkthrough for Rome

> **To the AI running this:** this file is your script and `STATUS.md` is your memory. Update it after every scan, decision and phase, not at the end. A human can follow this file by hand; every step is doable without an AI. Present the decisions conversationally, one at a time, and wait for answers. Adapt to your user's stack; never transplant a path or a name that does not fit it. **Set the expectation when you confirm the go-ahead:** the install is about 20 to 30 minutes; Phase 3, where you run one small real build through all eight steps, is another 45 to 90 minutes. One sitting, or two with `STATUS.md` as the bridge.

## What you are installing

**Rome** is a build protocol: the one way your user's AI builds anything for them (a skill, a script, a document set, a folder convention, a knowledge pack) or steps back on something already running. One phrase starts eight steps. Every step produces something and ends at the user's gate. The user's own words are the spec. A reviewer who did not write the plan checks the plan; a reviewer who did not build the thing checks the build.

| Piece | Job |
|---|---|
| **Eight steps, eight gates** | Rough Define → Research → Final Define → Plan → Check the plan → Build → Check the build → Ship. Every step ends with one line, "Step N of 8, <name>: <one line>. Approve?", and only the user's word passes it. |
| **Intake variables** | Six settings the AI fills from the user's first dump (mode, tier, what ships, entry point, second review, feedback loop). The user corrects; they never fill a form. |
| **Tiers 0 to 3** | Size, not calendar. Tier 0 hands off to a skill that already owns the pipeline. Tier 1 is one change in one sitting with no new files. Tier 3 is a folder of its own across chats, with a hand-off file at every retire. |
| **The user's words as the spec** | Their structure is quoted, never paraphrased. The AI's own scope lives in two labelled places only: "Beyond the ask" at step 1 and "Suggested additions" at step 2. |
| **Fresh eyes twice** | Step 5: a reviewer who did not write the plan red-teams it ("assume the plan is wrong"). Step 7: a reviewer who did not build it proves each done line with output, not prose. |
| **Findings in two buckets** | *Needs you* (Situation · Recommendation · Why) first, *Fixed* (no-brainers applied, vetoable) second. The user skims decisions, reads details only if they want to. |
| **Tripwires** | Eight questions the AI answers before every gate line; only the ones that fire get printed. |
| **Build on a copy** | A change to a live skill or a file people depend on is built in staging and installed at step 8 with one ask listing every file. |
| **The feedback loop** | One row per build in `runs.md`, and the skill file itself gets edited when a lesson should change the next build. |

The payload lives in `skill/` (the protocol in portable agent-skill format: `SKILL.md` plus two references) and `templates/` (a build STATUS, a hand-off file, a runs log), which Phase 2 installs beside the skill so they outlive this kit folder. `EXAMPLE-BUILD.md` walks one small build through all eight steps in about four minutes of reading; orient the user with it before the decisions.

---

## Phase 0: Environment scan

**Consent first, two sentences:** "To fit this to your setup I need to read your workspace layout and any standing-instructions file your AI already has, nothing else. OK to proceed?" On yes, establish these and record each in `STATUS.md`'s scan table before asking anything else:

1. **What am I?** Platform and capabilities: can I create files? run shell commands myself, or only hand them to the user to paste (record "shuttled")? spawn a sub-agent with no inherited context? persist memory across sessions? read my own context-window usage? Is there a second model I can call from the shell, my own or shuttled (a different vendor's coding CLI, read-only)?
2. **Where does the user's work live?** The folder, vault or repo where they would build things. Ask if nothing is visible from where you are running.
3. **Existing conventions.** A standing-instructions file (`CLAUDE.md`, `AGENTS.md`, `.cursor/rules/*.mdc`, a custom-instructions block, a "start here" note), and any project-folder convention (do their projects already carry a STATUS or README?). **Read them.** Phase 2 merges into them; it never overwrites them.
4. **Existing skills.** Does the platform discover skills from a directory it auto-loads, or must the protocol be referenced from a rules file, or pasted? If neither you nor the user can tell (no shell, unfamiliar app), record "unknown" and say so in the DP-6 line rather than defaulting silently; a chat app with a file connector (Claude Desktop) does not auto-discover. Do they already have a skill that turns a plan into a skill, builds knowledge packs, or exports kits? Rome calls those as-is at step 6, so note their names.
5. **Search.** Does the workspace keep a search index that must be refreshed after files move (a local index, a vault plugin)?

**Chat-only fallback:** if you cannot see a file system, narrate every step and the user creates the files. `STATUS.md` becomes a note they paste back at the start of each session. The protocol is unchanged.

---

## Phase 1: Decisions

Orient the user with `EXAMPLE-BUILD.md` first. Then work through these in order and record each in `STATUS.md`'s decisions table **before** moving to the next.

### DP-1: Where does a build's paper live?

A build produces paper: a Define, a plan, evidence, a hand-off. Rome needs one home for it at each tier.

**Options:**
- **A. The user's own project convention.** Tier 3 gets a build folder with `STATUS.md`, `research/`, `checks/`, `staging/` and `NEXT-CHAT.md`, laid out the way their existing projects are; tier 2 pastes the Define, plan and run card into the STATUS of the project it changes; tier 1 uses a scratch folder that is deleted at ship. *Trade-off:* the AI has to learn their convention first (Phase 0 item 3).
- **B. One `builds/` folder** at the workspace root, one sub-folder per build regardless of tier, each with the `BUILD-STATUS.md` template. *Trade-off:* tier-1 tweaks leave a folder behind each; the user has to clean up or accept the clutter.
- **C. One note the user keeps** (chat-only): the STATUS template lives in a note they paste at the start of each session. *Trade-off:* the user carries the memory by hand.

**Recommendation:** scan found a project convention with status files → **A**, mapped onto their names (their `STATUS.md` may be called `PROGRESS.md`; keep their name, map the job), plus one catch-all `_builds/STATUS.md` beside their project folders for a small build that no project owns yet, so two installs never invent two different homes. No convention → **B** at `<workspace>/builds/`, and write the catch-all status file for tier-1 and tier-2 builds that own nothing at `<workspace>/builds/STATUS.md`. No file access → **C**. Default if the user says "whatever you recommend": A if the scan found a convention, else B. The originator runs A because every build of theirs already had a project home; B is the honest answer for someone starting from a flat notes folder.

**Downstream:** Phase 2 step 3 (the wiring line names the home); Phase 3 step 1 (where the first build's STATUS goes); the "catch-all status file" wherever `SKILL.md` names it.

### DP-2: Who is the second reviewer?

Steps 5 and 7 need a reader who did not write the plan and did not build the thing.

**Options:**
- **A. A different model, run read-only from the shell.** A second vendor's coding CLI reads the build folder and returns a `VERDICT:` line. *Trade-off:* needs a shell and a second subscription or API; the command in `skill/references/prompts.md` has to be adapted to that CLI's flags. A shell the user runs for you counts: if you can hand them a command to paste in Terminal and read back the output, A is open to you, one hop slower.
- **B. A fresh sub-agent of the same model** with the red-team brief and no inherited context. *Trade-off:* same blind spots as the author, partly offset by the adversarial brief; costs from the same budget.
- **C. A fresh chat window the user shuttles.** The AI writes the prompt to a file, the user pastes it into a new chat with the build folder attached, and brings the verdict back. *Trade-off:* two manual hops per check; otherwise as good as B, provided the prompt file carries only the named files and none of the AI's own reasoning, which is the one leak nothing else in the protocol catches.
- **D. The AI's own pass only.** *Trade-off:* not a fresh read. Catches formatting, rarely assumptions.

**Recommendation:** scan found a second model callable from the shell → **A** (the originator's setup: the second model costs nothing from the primary budget and, measured across nine builds, its findings were mostly real). No second model but sub-agents → **B**. Neither → **C**. **D is never the silent answer**: if D is all that ran, the gate line says "own pass only" so the user knows what was and was not checked. Default if the user says "whatever you recommend": A if the scan found a second model, else B if sub-agents exist, else C.

**Downstream:** Phase 2 step 1 (edit the command block in `prompts.md` to the chosen reviewer); `runs.md` review-log columns (empty under D).

### DP-3: Sub-agents, or one thread?

**Options:**
- **A. Named sub-agents with fixed model and effort:** a `researcher` (mid-cost, medium effort) for tier-3 research fan-out and transcript digests, a `builder` (mid-cost, medium) for one file from an approved plan and for one fixture cold-run at step 7, a `grep-reader` (mid-cost, low) for inventories and bulk parsing, a `checker` (strongest model, high) for red-teams and evidence when DP-2 chose B. Never an unnamed agent that inherits the session's effort. The four definitions ship in `templates/agents/`. *Trade-off:* the platform must support per-agent model and effort settings.
- **B. One thread.** The AI does research in sequence, builds, then re-reads its own output as a stranger before each gate. Step 7's fixture runs become the user opening a fresh chat per test case, or the AI reading its own skill cold in a new session. *Trade-off:* slower on tier 3 and the "fresh eyes" at 6 and 7 are weaker; correctness of the protocol is unchanged.
- **C. Chat-only.** As B, narrated.

**Recommendation:** sub-agents with per-agent settings → **A**, and cap the fan-out at every step (never more fixture agents than test cases; a plan names its ceiling, because one uncapped session once spent a quarter of a month's budget). Otherwise **B**. The cheapest model tier is never used without the user's permission; mid-cost at low effort covers simple work without a quality trade the user did not approve. Default if the user says "whatever you recommend": A if the scan found sub-agents, else B.

**Downstream:** Phase 2 step 2 (create the agent definitions only under A); `SKILL.md` step 6 and step 7 wording about dispatch stays as written under A and reads as "you, in sequence" under B.

### DP-4: How much feedback loop?

Rome improves by being run. The close line asks "Feedback loop: 1, 2, 3, or later?".

**Options:**
- **A. Keep the loop, default 3.** One row in `runs.md`, a re-read of `SKILL.md` for the one rule the run bent, and a fresh-eyes read of the shipped thing a day later. *Trade-off:* 10 to 20 minutes after each build.
- **B. Keep the loop, default 1.** The row only. *Trade-off:* the skill never changes unless the user pushes.
- **C. No loop.** Close line dropped. *Trade-off:* every build starts from the same theory; nothing learned lands.

**Recommendation:** **A** for anyone who will run Rome more than a few times: the originator's version of the protocol changed on nearly every one of its first ten runs, and every change came from a run row, not from theory. **B** for a user who says up front they will not read a runs log; a brand-new user who has said neither gets A and revisits after three builds. Never C. Default if the user says "whatever you recommend": A.

**Downstream:** `SKILL.md` § 1 (the printed default), § 6 (the close line's "usual" number); `runs.md` exists under A and B, not C.

### DP-5: How does a long build survive a chat that fills up?

Long chats degrade before they end. Rome retires a chat on purpose and re-enters from a hand-off file.

**Options:**
- **A. Read the number.** The platform exposes context-window usage; the AI reads it at every gate and applies the ladder in `SKILL.md` § 3 (under 30 percent continue, 30 to 40 retire at the next good gate, 40 or over retire now). *Trade-off:* needs the number to be readable from a file or a tool.
- **B. Retire by structure.** No number: a tier-3 build retires at every hand-off point the plan names, and never runs more than two steps past step 5 in one chat. *Trade-off:* sometimes retires early; never too late.
- **C. Chat-only.** New chat per gate at tier 3, with the hand-off pasted in. *Trade-off:* the most hops; the most reliable memory.

**Recommendation:** the number is readable → **A**. Otherwise **B**. The hand-off file (from `templates/NEXT-CHAT.md`) is written at every hand-off point under all three, whether or not the chat then retires: the retire is the AI's call on context, never a ceremony. Default if the user says "whatever you recommend": A if the scan found the number, else B.

**Downstream:** `SKILL.md` § 3 context check (delete the percentage ladder under B and C, keep the "retire at hand-off points" sentence).

### DP-6: Where does the protocol install, and what is it called?

**Options:**
- **A. Installed as a skill the AI auto-discovers:** copy `skill/` into the platform's skills directory as `rome/`; the frontmatter `description` is what makes it fire on "let's build X". *Trade-off:* path is platform-specific; lives on one machine unless the folder syncs.
- **B. Kept in the workspace and referenced from the rules file:** copy `skill/` to `<workspace>/_tools/rome/` and point the standing-instructions file at its `SKILL.md`. *Trade-off:* needs a nudge more often than A; travels with the workspace, which is the point for a team.
- **C. Kept as documents the user pastes** (chat-only). *Trade-off:* the user carries it by hand.

**And the name.** The protocol is called Rome ("Rome wasn't built in a day": the point is that a build has steps and gates, not a single prompt). The trigger phrases also include "build mode". Rename only if "Rome" collides with something in the user's world (a person, a client, a project); the cost is three edits (folder name, frontmatter `name:`, the wiring line).

**Recommendation:** platform auto-discovers skills → **A**. Otherwise **B**, inside the workspace where their builds live; on Claude Desktop that means B plus the app's project-instructions field carrying the wiring line (Phase 2 step 5). **C** only with no file access. Keep the name unless the scan or the user surfaced a collision. Default if the user says "whatever you recommend": A if the scan found a skills directory, else B at `<workspace>/_tools/rome/`; keep the name.

**Downstream:** Phase 2 steps 1 and 3; every `references/` path inside `SKILL.md` is relative to the skill folder, so no edit is needed for A or B.

---

## Phase 2: Install

1. **Install the protocol** per DP-6: copy `skill/` (`SKILL.md` + `references/prompts.md` + `references/research.md`) to the chosen location. Then adapt minimally, and record every edit in `STATUS.md`:
   - DP-2: in `references/prompts.md`, replace the command block under "second-reviewer command" with the real command for the chosen reviewer under A, or delete the block under B and C (the "How to run it" paragraph below it already carries those two paths).
   - DP-5: under B or C, delete the percentage ladder sentence in `SKILL.md` § 3 and keep "retire at the plan's hand-off points".
   - DP-1: `SKILL.md` § 1 defines the catch-all status file once, with the default `builds/STATUS.md`; replace that path with the DP-1 choice (`_builds/STATUS.md` beside the project folders under A). § 5 refers to it by name only, so one edit covers both.
   - Rename only terms that clash with the user's vocabulary.
2. **Install the agent definitions** (DP-3 A only). Copy the four files in `templates/agents/` (`researcher`, `builder`, `grep-reader`, `checker`) into the platform's agents folder and replace the model line in each with the platform's real model name for that class (mid-cost for the first three, strongest for `checker`). Skip under B and C.
3. **Install the templates** so they outlive this kit folder: copy `templates/BUILD-STATUS.md` and `templates/NEXT-CHAT.md` to `<skill install path>/templates/`. Then **create the runs log** (DP-4 A or B): copy `templates/runs.md` to `<skill install path>/references/runs.md`; its rows are format examples, replaced by the first real row.
4. **Create the builds home** (DP-1 B only): `<workspace>/builds/` with a `STATUS.md` that says "catch-all for small builds; one heading per build".
5. **Wire the standing-instructions file.** This is the stickiness step: an install that only creates folders dies at the user's first new chat. Merge into their `CLAUDE.md` / `AGENTS.md` / rules file, in their format:
   > **Building anything:** "let's build X", "build mode", "Rome", "step back on X" → run the Rome protocol at `<path to SKILL.md>`. Eight steps, each ends at my gate; my words are the spec; a build's paper lives at `<DP-1 home>`; nothing installs over a live file without one ask listing every file.

   **No such file yet?** Create the simplest one the platform reads, say which and why. **Does the platform read it at all?** Claude Code reads `CLAUDE.md`; Cursor reads `.cursor/rules/*.mdc` when the rule has `alwaysApply: true`; Codex and most coding agents read `AGENTS.md`. **Claude Desktop and any chat app with only a file connector do not auto-read a workspace file:** there the wiring line goes into the app's own project or custom-instructions field (the user pastes it; you cannot), it fires only in chats opened inside that same project, so tell the user to test the trigger there and not in a plain chat, and the fallback is that every build chat opens with "read `<path>/SKILL.md`". Confirm with the user how their AI actually receives standing instructions before relying on the wiring, and record the answer in `STATUS.md`. Put the wiring where the user's AI actually works and **tell them which file you edited.**
6. Record every install path in `STATUS.md`.

---

## Phase 3: First live run, something small and real

Run **one real build** through all eight steps. Not a toy, and not their biggest idea: a tier-1 or tier-2 build they were about to do by hand anyway. The best first candidate is the thing they were going to hand back to someone else because it felt like too much: a one-file skill, a short script that pulls or reformats something, a folder convention, a checklist.

1. **Pick it with the user** and say the tier and why in one line. If they name something huge, propose the smallest piece inside it and say why.
2. **Run all eight steps from `SKILL.md`.** Fill the six intake variables yourself; ask the three-to-six-question batch; write the run card; sweep inside and outside; lock the goal; plan; check the plan with the DP-2 reviewer; build on a copy; prove each done line; ship with the asks batched. Print every gate line in its exact shape and wait for the word each time. At tier 1 this fits in one chat and each gate is a line or two; do not inflate it.
3. **Verification test 1, the trigger.** Open a *fresh* session with no context about this install and say something in the user's own words, like *"let's build a <thing>"*, nothing that names Rome. With sub-agents: launch one and give it that sentence. Without: the user opens a new chat, types it, and brings back what happened. If the protocol loads and step 1 opens with the six variables and a question batch, the wiring works. If not, widen the trigger phrases in the description (or the wiring line) with the user's actual phrasing and retest.
4. **Verification test 2, the cold read.** In a fresh session, hand over only the paper the build left and ask three questions. Tier 2 or 3, from the build's STATUS: "What step of 8 is this build at, what is the locked goal, and what would the next chat do first?" Tier 1, from its `runs.md` row: "What was the locked goal, where does the built thing live, and did it ship?" A correct answer from the file alone proves the paper works as memory. Record both tests' sentences and outcomes in `STATUS.md`.
5. **First feedback-loop row.** Append the run to `runs.md`: what the build was, what the user corrected, what got in the way of the locked goal, whether the research was too much or too little. If a rule in `SKILL.md` got in the way, edit it now.

---

## Phase 4: Wrap

1. Walk the user through what is installed and where: the protocol, the reviewer setup, the agents (if any), the builds home, the runs log, the instructions-file wiring, and the build they just shipped.
2. Tick every phase in `STATUS.md`; empty the Blockers row or say plainly what is still open.
3. Leave the habit behind, one line: **"Every build starts with your words and ends at your gate. If the AI is building and you have not said 'approve' recently, it has left the protocol."**
4. **Preserve the record before anything else:** copy this kit's `STATUS.md` (scan results, decisions, install paths, test outcomes) to `<skill install path>/references/install-record.md`. Only then is this kit folder safe to delete; keeping it for re-reads is also fine.

---

## If things go wrong

- **A capability is missing** (no sub-agents, no shell, no second model, no context number): take the degradation path named in the decision point. Every step has a sequential, chat-only or by-hand form; none dead-ends.
- **The user's conventions conflict with this kit's names:** keep their names and map the jobs. `STATUS.md` can be `PROGRESS.md`; `NEXT-CHAT.md` can be `HANDOFF.md`. Record the mapping in the install record.
- **The user keeps answering the question batch and skipping the gate word:** that is expected. Apply the answers, re-ask the gate line alone, one line, and wait. Never treat an answered list as approval.
- **Two files disagree** (STATUS says step 6, the hand-off says step 4): stop, surface both lines, ask. Never advance through a contradiction.
- **The build wants to move the locked goal:** stop for a re-lock at the gate. A silent goal change is the failure the whole protocol exists to prevent.
- **A step fails twice:** do not loop. Note it in `STATUS.md` Blockers, take the fallback, and tell the user.
