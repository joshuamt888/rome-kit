---
type: build
read_first: STATUS.md
updated: YYYY-MM-DD
---

# Status: <build name>

**Rome step N of 8 · YYYY-MM-DD HH:MM** (update at every passed gate and at every retire). Mode <technical | knowledge> · Tier <1 | 2 | 3> · Ships <a finished thing | a process | a skill> · Entry <new | mid-flight> · Second review <on | off> · Feedback loop default 3.

## Current position

- YYYY-MM-DD: <one line per gate passed or retire, newest first: what happened, what changed, where the evidence is>

## Rough Define (step 1)

**Goal, the user's words:** "<1 to 3 sentences, quoted>"

**What it is / is not.** <one line each>

**The user's structure, quoted, in their order:**
1. "<their words>"
2. "<their words>"

**Batch answers (user, YYYY-MM-DD):** 1 <word> · 2 <word> · 3 <word>

**Beyond the ask:** 1 <item: why · what a hit changes> · 2 <item>

## Final Define (step 3)

**Locked goal:** <1 to 3 sentences, locked at step 3; a change stops for a re-lock>

**Definition of done** (each line proved at step 7 by output, never prose):
1. <checkable line>
2. <checkable line>

**Borrowed, with verdict and why it serves the goal:**
- <source> → **whole | part | spark**, because <one clause>

**Test set** (fixtures under `checks/fixtures/`, run on copies at step 7):
- T1 <case>: "<the ask>" → <what it must show>
- T2 <case>: "<the ask>" → <what it must show>
- T3 must not fire: "<the ask>" → <the trigger stays quiet>

**Open decisions, ruled <user, YYYY-MM-DD>: A lean (n) · B lean (n).**
- **A. <decision>.** Options: (1) <option: trade-off>; (2) <option: trade-off>. **Lean n**: <why>.

Self-review: <placeholders none · contradictions none · scope edge = … · ambiguity none>

## Plan (step 4)

| # | Task | Who | Produces | Gate |
|---|---|---|---|---|
| 1 | <task with files named> | <me / agent name / user> | <output path> | <step> |

Hand-off points: <after step N's close line>. Fan-out ceiling (tier 3): <agents per step>. Parked: <items that do not serve the goal>.

## Run card

- **Tier N.** Test: <the one-line test that picked it>.
- **Creates:** <every file the run will create, by path>.
- **Touches at step 8 only:** <every live file the install edits, by path>.
- **Checker prompts paste from:** this file § Final Define (or `00-SPEC.md` § Done list once it exists).
- **Mechanics:** (1) <thing it must do> · (2) <thing it must do>.

## Research questions (step 2)

1. <question>
2. <question>

## Board

**Done means:** <one line>.
- [ ] Step 1 Rough Define
- [ ] Step 2 Research
- [ ] Step 3 Final Define
- [ ] Step 4 Plan
- [ ] Step 5 Check the plan
- [ ] Step 6 Build
- [ ] Step 7 Check the build
- [ ] Step 8 Ship

> Parked: <items, each with the date and why>

## Blockers / open decisions

- none
