# Rome: prompts reference

Every prompt Rome fires: step 5's red-team brief and plan review, the optional Define review at step 3, step 7's evidence check and build review, and the findings format every check returns in. Each pass by the second reviewer writes one row to the review log (`runs.md`, review columns).

Slots in angle brackets are filled by the AI running Rome from the run card. "The second reviewer" is whatever your install chose at DP-2: a different model run read-only from the shell, a fresh sub-agent, or a fresh chat window the user shuttles.

## Step 5 · fresh red-team brief

The dispatcher's rule: the reviewer gets the locked goal, the done list and the plan only, wherever they live (a STATUS section, or `00-SPEC.md` once the Define outgrew a page), never this chat's reasoning.

Brief (reviewer-facing):

> You are a fresh reviewer. You did not write this plan. Read-only.
> Your job is to find what is wrong; agreeing with the plan is a failure of this task unless you can quote why every done line is safe.
> Locked goal: <the 1 to 3 sentences, pasted>
> Definition of done: <file and section>
> Plan: <file and section>
> Red-team the plan against the goal and the done list. In plain English, max 500 words: **Killer issues** (max 7, most important first: exact quoted line · which done line or rule it endangers · why, in one or two sentences; no redesign proposals) · **Reinvented wheel** (any task that builds what a tested tool already does; name the tool, or say none found) · **Test-set stress** (the ONE test-set item most likely to break the steps as written, the step line it breaks, why) · **What the plan does not carry across the chat break** (one to three lines) · **Verdict line** ("VERDICT: APPROVED" if no killer issue endangers a done line, else "VERDICT: REVISE").

The adversarial sentence matters: in one measured comparison, an explicit "agreeing is a failure" instruction cut reviewer capitulation from roughly a third of runs to a handful.

## Step 5 · second-reviewer command + plan-review prompt

Command shape for a shell-run second model. The install (DP-2) replaces this block with the real command for your reviewer; the worked example is OpenAI's Codex CLI, read-only, with the reasoning effort pinned on the command so a config change cannot silently lower it:

```bash
codex exec -s read-only --skip-git-repo-check -c model_reasoning_effort=high -C "<build folder>" -o "<verdict file>" "$(cat <prompt file>)" < /dev/null
```

Prompt: plan versus definition of done.

```
You are a read-only reviewer. Do not edit any file.

Read two things in the current directory: (1) <file and section holding the locked goal and the definition of done>; (2) <file and section holding the plan>. <One sentence on what this build is, for example "The plan describes how an AI assistant will build a markdown skill for its owner inside a notes workspace."> It is NOT code. Do not review it as code.

Red-team the PLAN against the DEFINITION OF DONE. Assume the plan is wrong. Look for exactly these failure types:
1. A done line (<the range, for example 1 to 9>) that no plan task produces evidence for.
2. A task with no owner, no output, or an output nobody checks.
3. An ordering problem: a task that needs something a later task produces, or a gate that cannot be honored where the plan puts it.
4. A hand-off gap: something that must survive the chat break that the plan does not say how to carry.
5. Scope creep: a task that does not serve the locked goal.
6. An internal contradiction between the plan and the locked goal.
7. A task that builds what a tested tool already does; name the tool.

Rules: quote the exact line for every finding. Max 7 findings, most important first, killer issues only; skip nitpicks. One or two sentences each. Plain English. Do not propose a redesign. Do not praise.

End with exactly one line: "VERDICT: APPROVED" if no finding of type 1, 3, 4 or 6 is present, otherwise "VERDICT: REVISE".
```

How to run it, by the DP-2 choice. **A, a second model:** fill the slots, write the prompt to a file, run the command with the build folder as the working directory (tier 1: the scratch folder), read the verdict file yourself. **B, a fresh sub-agent:** dispatch it with the prompt file and the build folder path only. **C, a fresh chat the user shuttles:** write the prompt to `checks/<step>-prompt.md`; the user opens a new chat, attaches or pastes the named files, pastes the prompt, and brings the reply back as `checks/<step>-verdict.md`. Under B and C the fresh eyes are only as fresh as what the prompt carries: the named files and nothing of this chat's reasoning. In every case, never take a relayed summary.

## Step 3 · Define review (optional)

```
You are a read-only reviewer. Do not edit any file.

Read <file and section holding the Define> in the current directory. <One sentence on what this build is.> It is NOT a codebase. Do not review it as code.

Review it as a plan for a build. Look for exactly these failure types, and nothing else:
1. Internal contradiction: two lines in the section that cannot both be true.
2. Ambiguity that would make two reasonable readers run a step differently (quote the line, say the two readings).
3. Missing gate or missing output: a step that does not say what it produces or who approves it.
4. Scope creep: anything in the section that does not serve the stated goal.
5. Unverifiable claim: a rule that cannot be checked at "Check the plan" or "Check the build".
6. A test-set mismatch: name one item in the test set that the eight steps, as written, would not fit, and say why.

Rules: quote the exact line for every finding. Max 8 findings, most important first. One or two sentences each. Plain English. Do not propose a redesign; name the problem. Do not praise.

End your response with exactly one line: "VERDICT: APPROVED" if nothing in findings 1, 3, or 6 is present, otherwise "VERDICT: REVISE".
```

Off by default at step 3; propose it on a long or contested tier-3 Define.

## Step 7 · evidence prompt

For a fresh reviewer that did not build the thing:

```
You are a fresh reviewer. You did not build this. Do not edit, fix, or improve anything; read-only.

Run the deliverable. For each definition-of-done line, show the actual output or behavior that proves it. No output = not done. Assertions ("it works") are not evidence. Commands and their results are. If the deliverable is a markdown skill, "run" means: follow the skill cold on the real prompt given below, and treat that transcript as the run. If it is a knowledge build with nothing to run, the evidence is exact quotes from its files.

Locked goal: <the 1 to 3 sentences, pasted>
Definition of done: <file and section>
Real prompt (skills only): <prompt>
Deferred to step 8 (report as DEFERRED, not FAIL): <the done-line numbers the plan assigns to step 8>

Also flag anything in the deliverable that does not serve the locked goal.

Technical mode: the proof is the running thing or its test output, never prose about it.

For each definition-of-done line (in order), produce one row:
- the line number and its text
- the evidence: an exact quote from the files, or the command you ran and its output
- a verdict: PASS, FAIL, DEFERRED (a line named above as step 8's), or UNPROVABLE-HERE (evidence would require a live run this read-only session cannot perform)

Return the table only. No summary, no praise, no redesign proposals.
```

## Step 7 · build-review prompt (second reviewer)

```
You are a read-only reviewer. Do not edit any file.

Read the built files in the current directory, together with the locked goal and the definition-of-done list that govern this build, in <file and section, absolute path>. <What the deliverable is: a built markdown skill an AI assistant runs for its owner · a knowledge pack of markdown pages the AI reads to answer questions · a kit · a script>. It is NOT a codebase. Do not review it as code. Done lines <numbers> are step-8 ship tasks that run after this review, by design; do not report them as missing.

Review the built files against the definition of done. Look for exactly these failure types, and nothing else:
1. A done line with no visible support in the files: quote the done line, say what support is missing.
2. Internal contradiction: two lines in the files that cannot both be true.
3. Ambiguity that would make two reasonable readers run a step differently (quote the line, say the two readings).
4. Scope beyond the locked goal: anything in the files that does not serve the stated goal.
5. Unverifiable rule: a rule that cannot be checked by any evidence the definition of done calls for.

Rules: quote the exact line for every finding. Max 8 findings, most important first. One or two sentences each. Plain English. Do not propose a redesign; name the problem. Do not praise.

End your response with exactly one line: "VERDICT: APPROVED" if no finding is present, otherwise "VERDICT: REVISE".
```

Run it with the built thing's folder as the working directory (the skill folder, the kit, the pack); name the spec by absolute path so a read-only reviewer can read outside its folder.

Verdict rule: any finding → REVISE. All five types are defects in a built thing, not nitpicks. Expect the first run on a real build to return several findings with about half of them real; that ratio is the reviewer earning its place.

## Findings format (steps 2, 5 and 7)

The shape every check returns in:

```
Needs you:
#1 · Situation: <what is wrong, plain English>
     Recommendation: <the one lean>
     Why: <one or two sentences>

Fixed (applied; veto any):
- <one line per no-brainer>
```

Decisions first, so the user can skim; details and file paths last. No niche term without a definition in the same sentence.
