# EXAMPLE-BUILD: one small build through all eight steps

A worked example so the eight steps are concrete before you decide anything. Invented business, real shape. Four minutes of reading.

**The user:** runs a three-person design studio. **The dump:** "I want a kickoff-pack skill. When I paste a client intake call transcript, it should give me a project folder with a brief, a rough timeline, and the first email to the client. I do this by hand every time and it takes an hour."

## Step 1 · Rough Define

The AI prints the six variables in one line: *knowledge mode · tier 2 · ships a skill · new · second review on · feedback loop 3.* Then the Rough Define, the user's structure quoted:

> Goal: "a kickoff-pack skill… a project folder with a brief, a rough timeline, and the first email."
> Structure: 1 "paste a client intake call transcript" · 2 "a brief" · 3 "a rough timeline" · 4 "the first email to the client".

**Question batch** (assumption plus lean, answered by number):
1. The folder lands in your existing `Clients/<name>/` tree, not a new root. Lean: yes.
2. The timeline is phases with rough durations, not dates. Lean: yes; dates need the calendar.
3. The email goes out in your voice. Lean: a draft you edit, never sent by the AI.
4. Done means: three files in the folder and the email draft, from one real transcript. Lean: yes.

**Beyond the ask:** 1. Look at whether an existing transcript-to-brief skill already does the first two files (a hit would cut the build in half). 2. Check what the last five kickoff emails had in common (a hit becomes the email template).

**Run card:** tier 2, test: one new skill, one chat. Creates `Clients/_skills/kickoff-pack/SKILL.md` and its fixture. Touches at step 8: the standing-instructions file (one line). Checker prompts paste from the studio's `Projects/STATUS.md` § Kickoff pack. Mechanics: (1) parse a transcript into named fields · (2) stamp a folder from a template · (3) draft an email from fields.

User: "1 yes 2 yes 3 yes 4 yes. Approve."

## Step 2 · Research

Inside sweep: the studio already has a `client-folder` template; borrowed **whole**. Outside sweep, per mechanic: (1) transcript-to-fields: a registry skill exists, opened, verdict **part** (its field list; its prose is generic); (2) folder stamping: the existing template covers it, **whole**; (3) email drafting: **build it**, searched "kickoff email template skill", nothing worth reading.

Light check: answered the brief; research sized right for tier 2; what argued against the lean: the registry skill wants a fixed transcript format, ours vary. **Suggested additions:** 1. A "what we still need from the client" list as a fourth file; the last five transcripts each had one open question the studio chased later. Lean: add it.

User: "Add 1. Approve."

## Step 3 · Final Define

**Locked goal:** one skill that turns a pasted intake transcript into a client folder holding a brief, a phase timeline, an open-questions list, and a draft first email in the studio's voice.

**Done list:** 1. A real transcript produces four files in `Clients/<name>/`. 2. The brief names client, scope, budget range and deadline, each traced to a transcript line. 3. The timeline is phases with durations, no dates. 4. The email is a draft file, never sent. 5. A pasted text that is not an intake call does not fire the skill.

**Test set:** T1 last week's real intake call; T2 a transcript with no budget mentioned (the brief must say "not discussed"); T3 must not fire: a pasted supplier quote.

Open decision A: one skill or two (parse, then stamp). Options with trade-offs; lean: one, because tier 2 and one user. User: "One. Approve."

## Step 4 · Plan

| # | Task | Who | Produces | Gate |
|---|---|---|---|---|
| 1 | Write `SKILL.md` from the locked goal | builder agent | the file, in staging | 6 |
| 2 | Write fixtures T1 to T3 | the AI | `checks/fixtures/` | 6 |
| 3 | Cold-run each fixture on the staged skill | builder agent ×3 | `checks/step7-T1..T3.md` | 7 |
| 4 | Evidence check, done lines 1 to 5 | second reviewer | `checks/step7-review.md` | 7 |
| 5 | Install the skill; one line in the instructions file | the AI, one ask | the live skill | 8 |

User: "Approve."

## Step 5 · Check the plan

Second reviewer (read-only): two findings. *Needs you* #1: done line 2 says "traced to a transcript line" but no task produces the trace; recommendation: the brief carries a line number per field; why: otherwise line 2 cannot be proved at step 7. *Fixed:* T3's fixture said "an invoice", changed to "a supplier quote" to match the Define. Verdict: REVISE → fixed → user: "Approve."

## Step 6 · Build

The builder writes the skill in `staging/`. Plan change 1: the email draft gets a `Subject:` line the Define did not mention; why: the studio's last five emails all had one; learned: read the examples before the spec. The AI verifies the staged file against the done list. User: "Approve."

## Step 7 · Check the build

First line of the gate: **4 of 5 done lines proven by output today; line 5 waits on the install (deferred).** T1 produced four files; T2's brief reads "Budget: not discussed"; T3 did not fire. The reviewer's table: lines 1 to 4 PASS with the file paths and quoted lines; line 5 DEFERRED. One fix from the review: the timeline had a date in it. Fixed, re-checked, user: "Approve."

## Step 8 · Ship

"Anything you've been meaning to add? Cheaper now than after install." User: "No." Ask 1: install `kickoff-pack/` over the studio's skills folder (three files listed) and add one line to the instructions file (diff on disk). Gate line: "Step 8 of 8, Ship: filed and handed off. Approve?" Close line: "Done. Feedback loop: 1, 2, 3, or later? (usual: 3)". User: "Approve. 3." The real trigger run proves line 5. One row in `runs.md`: corrections none; what got in the way: nothing; research sized right.

Elapsed: about 70 minutes, one chat.

## The same shape for other builds

| The build | Mode | Tier | What "run the deliverable" means at step 7 |
|---|---|---|---|
| A script that pulls invoices from a chat app into a folder | technical | 2 | The script runs on a real week; the folder has the files; the count matches. |
| A knowledge pack digested from a book | knowledge | 3 | A fresh session answers three domain questions from the pack alone and cites pages. |
| A folder convention for client projects | knowledge | 1 | A fresh session reads one folder and states what each file is for, from the README alone. |
| Stepping back on a process already running | either | mid-flight | § 2 Reconcile first; steps already evidenced are accepted as done, the rest re-run. |
