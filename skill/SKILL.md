---
name: rome
description: Use when the user wants to build something with their AI, or step back on something already running. Triggers on "Rome", "build mode", "/rome", "let's build X", "step back on X", and mid-flight re-entry like "Rome, we're mid-flight on X". Covers everything from a 30-minute tweak to a build that spans several chats: eight steps, each gated by the user, with the user's own words as the spec and fresh eyes on every plan and every result. Not for running a pipeline another skill already owns end to end; Rome names that owner at step 1 and hands off.
---

# Rome wasn't built in a day

Rome is the single way your AI builds anything for you, or steps back on something already running: a skill, a document set, a script, a folder convention, a knowledge pack. One phrase starts eight steps. Every step produces something and ends at your gate. Your own words are the spec. A reviewer who did not write the plan checks the plan, and a reviewer who did not build the thing checks the build.

Written to the AI running it. "You" below is the AI; "the user" is the person it builds for.

Mode: **orchestrator** where the platform allows it. You plan and verify; sub-agents research, draft and check. Each sub-agent gets a fixed model and effort in its brief, never the session's default. On a platform without sub-agents, you do every step yourself in sequence and say so at step 1.

---

## 1. Intake (set at step 1)

Fill all six from the user's dump with your own picks and print them in one line at the step-1 gate. The user corrects what is wrong, nothing more. They should never have to do the heavy lifting.

- **Mode:** technical · knowledge. Changes one thing: the step-7 proof. Technical = the running thing or its test output. Knowledge = file text quoted per done line.
- **Tier:** 0 hand-off · 1 small · 2 medium · 3 large.
- **What ships:** a finished thing · a process that keeps running (then the plan names its runner and its maintenance hook: who runs it, when, how you know it broke) · a skill.
- **Entry point:** new · mid-flight (then § 2 runs first). "Step back on something already running" is mid-flight, nothing separate.
- **Second review:** on · off. Off only when no second reviewer is available or the user says so; otherwise steps 5 and 7 always get one.
- **Feedback loop after the build:** default on. Printed here, asked only at the close line.

**Tier 0: hand off and stop.** Ask: *a run of an existing pipeline, or a change to it?* A run of a pipeline another skill already owns end to end belongs to that skill. Say so in the step-1 gate line ("Step 1 of 8, Rough Define: tier 0, this belongs to `<skill>`. Approve?") and stop there. A change to that pipeline is a Rome build, sized like any other.

**Tiers 1 to 3.**
- **1, small.** One file or one change, one sitting. All eight steps and gates, each a line or two. No new files in the user's workspace: the checkers get one scratch folder (`rome-<build slug>/`), deleted at step 8, after its locked goal (verbatim) and where the built thing landed are written into the build's `runs.md` row, the only paper a tier-1 build leaves. If a retire is forced mid-build, copy the scratch Define, plan and evidence into the catch-all status file first (the scratch folder is session-bound).
- **2, medium.** A few files or one new thing, one chat. Define, plan and brief live in the status file of what the build changes; if nothing owns it, the catch-all status file.
- **3, large.** A folder of its own, usually more than one chat. Tier is a *size*, not a calendar: a large build can pass its gates in one evening when the user is decisive. Hand-off file plus § 2 at each re-entry; `research/` folder only if research ran; Define and plan in the build's STATUS until one outgrows a page (§ 5).

The templates for a build's STATUS and hand-off live beside this skill at `templates/` (the installer copies them there; until then, the kit's own `templates/` folder); the run log at `references/runs.md`. The catch-all status file for small builds that own nothing is `builds/STATUS.md` at the workspace root unless the install named another.

---

## 2. Reconcile: at mid-flight entry and every tier-3 re-entry

1. Re-read the state files once: STATUS, Define, plan, hand-off.
2. **Any conflict → stop, surface it, ask the user to resolve. Never advance through a contradiction.**
3. Step 1's input is those files plus the user's re-entry words: their words quoted, file text cited by file.
4. Steps already evidenced in the files are listed as *accepted as done*, not re-run; the user confirms that list at the first gate after re-entry. A gate may stay open for days; STATUS's "Rome step N of 8" line says where it stands.

---

## 3. The eight steps

Every step the build runs produces something and ends at the user's gate, every step, every tier (tier 0 runs step 1 only). Every gate line has one shape, **"Step N of 8, <name>: <one line>. Approve?"**, and always comes after the tripwires (§ 4).

**Context check at every gate.** Before the gate line, read how full your context window is, if the platform exposes it, and print "Context NN percent: continue / retiring after this gate". Under 30 percent continue. 30 to 40, retire at the next good gate (after step 1 on tier 3, after 3, after 5, after 7, before the feedback loop). 40 or over, retire now, hand-off written. Never retire between 4 and 5, mid-6, or between 7's findings and their rulings. Context quality degrades well before the window fills. If the platform does not expose the number, retire at the plan's hand-off points instead (§ 5).

**A gate is approved only by the word.** An answered question batch or a *Needs you* list is never the approval. When the user answers the list and skips the gate line, apply the answers, re-ask the gate line alone, one line, and wait.

**Gate output is layered for a skim.** The gate line and *Needs you* first, the *Fixed* list next, details and file paths last. At step 7 the first line is the score: N of M done lines proven by output today, and what each unproven one waits on. On a build the user calls low-stakes they may approve on trust; the gate stays, the depth of their read is their call.

### Step 1 · Rough Define
**What.** Organize the user's dump: a 1 to 3 sentence goal in their words, what it is / is not, their structure quoted word for word, the six intake variables, the questions research must answer, and the Beyond-the-ask list. Tier 0 is called here.
**Rule.** The user's structure is the spec, quoted, not paraphrased. Never build inside a dump; route it to a home first. **Brainstorming pass, every run:** after organizing, ask three to six numbered questions even when the dump reads complete. Each is one you would otherwise settle alone (purpose, a constraint, what done looks like, a scope edge, an assumption the dump leaves open), written as the assumption plus your lean, so the user answers by number with a word. Every further gap joins the same batch, repeated until no gaps. The batch is answered before the gate line is asked, and its answers are not the approval.
**User.** Hands over the dump or the re-entry words; answers the batch in one dump.
**You.** Organize their words without adding to them; your own scope goes only under Beyond the ask. Output shape: Goal · Context · Inputs · Constraints and don'ts · Deliverables · Open questions (what research must answer) · **Beyond the ask**: the research you will run that the user did not name, as many numbered items as the build earns and none for show, each with one line on why and what a hit would change. Every item runs unless the user strikes it by number ("not 4 and 5"). This is where you make executive calls: "I want to learn more about X, so I'll look into it and see if it's worth pursuing."
**Produces.** Tier 1: a line or two in chat. Tiers 2 and 3: the Rough Define in STATUS. **Run card**, every tier, closes the step-1 output and every later step reads from it: the tier with the one-line test that picked it · every file the run will create or touch, by path · the file and section steps 5 and 7 paste into the checker prompts · the build's **mechanics**: the two to six things it must *do* (parse X, move Y, check Z, run on a schedule), each the unit the step-2 outside sweep searches for.
**Gate.** "Step 1 of 8, Rough Define: goal, structure, variables, research questions, beyond the ask. Approve?"

### Step 2 · Research
**What.** Two lookups (the sweeps below) at every tier, inside the workspace first. Outside *research* by tier: none at 1, web at 2, deep at 3.
**Rule.** Two sweeps run every time, every tier; they are lookups, not research. **The outside sweep searches the mechanic, not the thing**: one lookup per run-card mechanic, in order, stop at the first that holds: already installed? → a skills registry (for example `npx skills find "<mechanic>"`) → one GitHub search. Look for "a skill that's similar, or even completely different, but there are mechanics in it that are the same." Why: a YAML frontmatter parser was hand-rolled twice in one workspace with a YAML library installed the whole time, because the search was for "skill builder", never "frontmatter parser". Knowledge mode sweeps only mechanics that are scripts or repeatable structures; a three-sentence prose mechanic costs more to borrow than to write, and the brief says which were skipped. The brief follows `references/research.md`: the lean and what would change it *before anyone looks*; only the brief's questions, with the Beyond-the-ask items the user left standing as questions in their own right; extras under "Found, not asked"; ends with "What argued against the lean" and then "Suggested additions". A source counts only if the answer would flip. Content research a tool does for its own output (a pack builder digesting a book) is that tool's job at step 6, not this step. **Sized to the build:** full research only when the build warrants it. **Light check at this gate:** your own pass, no fresh agent: answered the brief? too much or too little? what argued against the lean? In the step-5 findings shape.
**User.** Rules only on what the brief or the light check flags, and on any source you propose beyond the tier's default (a deep pass on a tier-2 build, a book, a video, a person).
**You.** Write the brief; at tier 3 fan out sub-agents, at tiers 1 and 2 work alone. Verdicts on existing work come back per mechanic as whole / a named part / spark / build it (nothing fit; the brief says what was searched). Only the named part of a borrowed skill is read into the chat, and the plan lists every borrowed part. Run the light check. Then write **Suggested additions**: numbered, drawn from anything the research surfaced, each = the finding that prompted it · what adding it would change · your lean. The user rules by number at the gate; an accepted item enters the step-3 Define as scope, a declined one goes to the parked list, and nothing on the list is built unaccepted.
**Produces.** Tier 1: the sweep result in a line or two. Tier 2: brief and findings in STATUS. Tier 3: a `research/` folder.
**Gate.** "Step 2 of 8, Research: the lean, what argued against it, suggested additions. Approve?"

### Step 3 · Final Define
**What.** Goal re-cut to 1 to 3 sentences and **locked**; definition of done, every line checkable; what you take from existing work (whole / a named part / spark) and why each serves the goal; the build's test set: two to five real cases, more on a large build, walked on paper at step 5. A build that wires a trigger (a standing-instructions line, a hook, a route) adds one case the wiring must *not* fire on. A build that re-cuts numbers writes its stale-number case over every output a reader opens, each named by path in every format it ships in, never only the decision papers. When the dump names how the user will judge the result ("I'll go through my texts"), that sentence is its own done line, quoted, and step 7 runs it before the gate; a narrower technical proxy in its place has cost a mid-build re-lock before.
**Rule.** The locked goal is what steps 5 and 7 check against; a change that would move it stops for a re-lock. Anything unsettled is written as `[NEEDS CLARIFICATION: question]`, never guessed. **Brainstorming pass:** every open decision gets two or three approaches with trade-offs and your lean, the alternative the research surfaced always among them, shown before the pick, batched. Then self-review: placeholders, contradictions, scope, ambiguity.
**User.** Locks the goal or re-cuts it, and rules on the options.
**You.** Re-cut, write each done line so it can be proved, list every borrowed part with its verdict. A second-reviewer read of the Define is off by default; propose it at tier 3 when the Define is long or contested (prompt in `references/prompts.md`).
**Produces.** Tier 1: goal plus done list, a few lines. Tiers 2 and 3: in STATUS (§ 5 for when it becomes `00-SPEC.md`).
**Gate.** "Step 3 of 8, Final Define: goal, done list, test set. Approve?"

### Step 4 · Plan
**What.** Tasks, who does each (you / a sub-agent / the user), what each produces, hand-off points if it spans chats. A tier-3 plan names its fan-out ceiling (agents per step); a step that would exceed it stops for the user's word.
**Rule.** No placeholders: every task names its files and owner and is small enough to finish. The plan lists every borrowed part. A process that keeps running gets its runner and maintenance hook named here. A build whose scripts write to protected apps (contacts, messages, mail, calendars) names the hand-back as a user step and says which writes may bounce off a permission prompt.
**User.** Approves, or marks what to change.
**You.** A table: task · who · produces · gate. Name every hand-off point. Park anything that does not serve the goal.
**Produces.** Tier 1: a few lines. Tiers 2 and 3: in STATUS (§ 5).
**Gate.** "Step 4 of 8, Plan: tasks, owners, hand-offs. Approve?"

### Step 5 · Check the plan
**What.** Three checks, every tier: the second reviewer (read-only, ends with a `VERDICT:` line), your own pass, and the test set walked on paper. When no second reviewer exists, a fresh agent or a fresh chat with the red-team brief stands in; when neither exists, say in the gate line that only your own pass ran. Findings fixed before the gate.
**Rule.** The reviewer gets the locked goal, the done list and the plan only, never this chat's reasoning. **"Assume the plan is wrong. Return killer issues only."** Strategic challenge first, correctness last. Read each reviewer's own output, never a relay. **Findings reach the user in two buckets, one shape:** *Needs you* first, each judgment call as Situation · Recommendation · Why; then *Fixed*, no-brainers applied, one line each, the user can veto. Never an edit to the locked Define, which is always *Needs you*, even its proof text. At tier 1 the prompts and outputs are short.
**User.** Nothing until the findings come back; then rules on *Needs you*.
**You.** `references/prompts.md` for the red-team brief and the reviewer command, slots filled from the run card; own pass; test-set walk; one row in the review log. At tier 1 there is no build folder: write the goal, done list and plan into one scratch folder (`rome-<build slug>/`, the folder the reviewer runs in) for the checkers at steps 5 and 7, and delete it at step 8.
**Produces.** Findings in two buckets, the plan changes for the gate, one review-log row.
**Gate.** "Step 5 of 8, Check the plan: findings and both verdicts. Approve?"

### Step 6 · Build
**What.** Sub-agents build; you verify. Without sub-agents, you build, then re-read your own output as a stranger before the gate.
**Rule.** Plan changes logged one line each (what / why / learned), approved at this step's gate. Anything that would move the goal stops for a re-lock. Scope that does not serve the goal goes to the parked list, never into the session. Prompts live on disk, not in chat. **A change to a live skill or a live file people depend on is built on a copy, never in place:** tiers 2 and 3 in `<build>/staging/`, tier 1 in the scratch folder; checked on the copy; installed at step 8 with one ask listing every file. Your own tools are called as-is at this step (a skill-structuring tool for skills, a pack builder for knowledge packs, a kit exporter for kits, a voice skill for anything sent in the user's name); Rome does not re-run their research or checks.
**User.** Rules on anything that would move the goal.
**You.** Dispatch the named agents in parallel where the platform allows. Any step that runs on the machine's own CPU (a transcription, a PDF render, an embedding run) is serialized even when different agents own the tasks around it, and the plan lists those steps in sequence. Log plan changes; park non-goal scope.
**Produces.** The built thing, the plan-change lines, the parked list. Tier 3: a retire entry in the build's log at each retire.
**Gate.** "Step 6 of 8, Build: the built thing and its plan changes. Approve?"

### Step 7 · Check the build
**What.** For each done line, the actual output that proves it, by someone who did not build it: the second reviewer first, a fresh agent or fresh chat when there is none, your own pass with fresh eyes when there is neither, stated as such. Logged.
**Rule.** **"Run the deliverable. For each definition-of-done line, show the actual output or behavior that proves it. No output = not done."** No completion claims without fresh verification evidence. By what ships, in either mode. Technical: the running thing or its test output, never prose about it. A skill: the test set is the run; one fresh agent per case follows the skill cold from its fixture, on copies, never a live skill; fixture agents are capped at the test-set size, on a mid-cost model, never one top-model agent per case; the evidence checker then maps each done line to those transcripts and re-runs any command it needs. A knowledge build that is not a skill: file text quoted per done line. Findings in the step-5 buckets and shape. **The evidence is pinned to what it measured:** it names each artifact by path and by the measured value it proved; any edit, rename or requirement landing after the evidence re-opens the done lines that cite that artifact and re-runs them before step 8; a late requirement that changes a locked term edits the Define's superseded text, never only a plan change beside it.
**User.** Rules on *Needs you*.
**You.** `references/prompts.md` for the evidence prompt and the build-review prompt, slots filled from the run card; the done lines the plan assigns to step 8 are named in both prompts as deferred and come back DEFERRED, not FAIL; read each reviewer's own output; log row. Hold every fix until all checkers have returned, then one fix pass and a re-check of the changed lines only (editing mid-check leaves the evidence table stale). A re-check that finds residues the fix pass introduced gets one more pass, each edit verified against the raw source, never a third; anything still standing goes to *Needs you* at the gate.
**Produces.** Evidence per done line, every reviewer's output, one review-log row.
**Gate.** "Step 7 of 8, Check the build: evidence per done line. Approve?"

### Step 8 · Ship
**What.** File it · use-case lines for anything installed ("use X when Z") · the hand-off if it continues · the feedback loop.
**Rule.** "File it" = the build lands in its permanent home under the user's own folder conventions. File it also reads the target of every pointer the build installed or touched, fixing a dead or wrong one before the asks or sending it to *Needs you*, and refreshes any search index the workspace keeps when the build created, moved or deleted files, before the real trigger run (a stale index once served a deleted page to a trigger test). Use-case lines are written for the user, per install, in their terms. The tier-3 hand-off (`NEXT-CHAT.md`, template beside this skill in `templates/`) carries five things: do-not / closed list · read-first order · every rule attributed to a person and a file · the first action, written as an action the reader may take, never a send, attach or invite · a model and mode line. At tiers 2 and 3, STATUS carries "Rome step N of 8" with the time the gate passed; update it at every passed gate and at retire; tier 1 has no STATUS line. Every touch to infrastructure (the AI's config, skills, hooks, standing instructions) gets its own numbered ask, all in one batch, each ask covering exactly what its heading names, its diff on disk (`checks/step8-asks.md` in the build folder; tier 1: the scratch folder), do-and-report items under their own heading. The user answers once, by number or "all leans".
**User.** Answers the batch once: a number per ask, or "all leans".
**You.** Before the asks, close the evidence file against the last edit: one section that restates every done-line verdict as it stands after the final fix pass, gives every reviewer flag and every fix-pass residue a one-word disposition (fixed, with its grep · accepted, as built or as written, with the word that accepts it · carried, with the file it went to), and edits the Define's own text for any locked term the build broke, never a note beside it. Then close the rules: every rule the run created or changed has one owner file, dated and attributed, and every other file that states it is edited in place with the superseded text marked. Then audit the hand-off itself: every number, rule, model choice and first-action parameter in NEXT-CHAT is listed, repeated numbers are identical, and a first action that depends on anything not written there sends the hand-off back. Then open each file the hand-off's read-first list names and confirm it holds the claim made for it. Then paste the user's gate words sentence by sentence into `checks/step8-asks.md` with one disposition each: carried (file and line), not carried (why), or open (goes to the hand-off's open list, never its closed list); a summary of the gate drops objections and hardens hedges. Then file it, write the use-case lines, write the hand-off, print the close line; the user's answer to it starts the feedback loop.
**Produces.** The shipped thing in its home, the use-case lines, the hand-off at tier 3.
**Gate.** Step 8 is the one step whose gate line comes last (with the gate and close line above the asks, users answer only the close line). Order: first one line, "anything you've been meaning to add? cheaper now than after install"; an answer that keeps the goal lands as a plan change before the install, one that moves it stops for a re-lock. Then the numbered asks with their diffs on disk. Then two named lines: the gate line "Step 8 of 8, Ship: filed and handed off. Approve?" and the close line (§ 6). The user answers everything once ("all leans, yes, 3"). Their answers are written back into `checks/step8-asks.md` under an Answers heading with the date and their words, and the hand-off names each ask's state: done, owed to the user, declined.

---

## 4. Tripwires

Answer all eight before every gate line, at every step, at every tier, and print only the ones that fire, plus one line, "Eight tripwires checked". A tripwire that fired and was handled still prints, with how it was handled.

1. Am I stating as decided something the user only implied?
2. Am I past the literal ask anywhere other than Beyond the ask (step 1) and Suggested additions (step 2), the two labelled places my own scope is allowed?
3. Is this their quote or my paraphrase?
4. Did I read every number back, the same in every file the run card ships, with the losing value marked inline where it sits ("$18K (superseded YYYY-MM-DD, see …)"; the Define alone is edited, never marked, per step 8)?
5. Did I read the reviewer's own output, not a relay?
6. Did I show the list before the pick?
7. Is this plain English, no task code, ID or shorthand without its meaning in the same sentence (a gate file has to stand alone from STATUS)?
8. Did I read back every rule this step changed across every file that states it, inside the edited file and in every skill whose own text states the same rule?

---

## 5. Standing rules

- **Questions come batched**, so the user answers in one dump. Never two questions at a time.
- **Files follow steps, never a stub.** Define, plan and brief live in STATUS until one outgrows a page; name the new file in the gate line and the gate's approval is the ask (new files ask first), then it gets its own file (`00-SPEC.md` for the Define). Folder mechanics come from the user's own project conventions; Rome does not restate them.
- **Reviewers: a different model first, then the strongest model you have.** A second model at steps 5 and 7 costs nothing from the primary model's budget and its findings are mostly real. The fresh red-team (step 5) and evidence checker (step 7) run on the strongest model at high effort only when the second model is down, at its limit, or the user asks. Mid-cost models draft; the cheapest tier never without permission.
- **Hand-off points are where a retire is possible, not required.** At every hand-off point the plan names and at every step-8 close line, the hand-off is written and echoed, then the context ladder in § 3 decides. The retire is your call, unprompted, on context, never on ceremony.
- **Dated follow-ups a build schedules are yours to remember.** When the user asks for a check on a date ("schedule an analysis for 7 days from now, I don't want to have to remember it"), it lives in persistent memory with the window and their exact question; the first Rome run inside the window asks it once, at its first gate, then the note is deleted. Without persistent memory, it goes in the catch-all status file's open list.
- **Adjustments land through the feedback loop, not in chat.** All of this is theory until a real run gives feedback. Each loop asks what got in the way of the locked goal, whether the research was too much or too little, and, on tier-1 runs, which steps went deeper than the build needed. Append one row to `references/runs.md` per build; edit this file when a lesson should change how the next build runs.

---

## 6. Close line

Printed in the same message as the step-8 gate, exactly:

Done. Feedback loop: 1, 2, 3, or later? (usual: 3)

1 = one row in `runs.md`. 2 = the row plus a re-read of this skill for the one rule the run bent. 3 = the row, the re-read, and a fresh-eyes read of the shipped thing a day later. When step 6 called another skill, the line names it too (`Done. Feedback loop: rome + <skill>: 1, 2, 3, or later?`) and the user's answer sets the depth per skill.
