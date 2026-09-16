# Rome: research reference (step 2)

What step 2 needs that does not fit in `SKILL.md`: the brief template, the three research tiers and the sources allowed at deep, the two sweeps, the source rule, and how borrowed work is graded.

## Brief template

Six headers, in order:

1. **The lean going in.** The working guess, stated plainly, before any research happens.
2. **What would change the lean.** The specific findings that would flip the plan, written before anyone looks. Always carries one standing question: *what do the strongest existing tools do here, and does it differ from the lean?* Name the alternative and what switching costs; the answer feeds step 3's option list.
3. **Questions → who → where → output.** A table: each question, which agent (or "me") answers it, what file the answer lands in. The step-1 Beyond-the-ask items the user left standing sit in this table marked *AI's own*, under the same rules.
4. **Rules every researcher gets.** Answer only your question; extras go under "Found, not asked."
5. **Budget.** Headcount, wall-clock, any paid-credit ceiling.
6. **Not researching.** Named exclusions, so scope cannot creep.

The brief ends with **"What argued against the lean"** and then **"Suggested additions"**: numbered, from anything the research surfaced, each = finding · what adding it changes · the AI's lean. The user rules by number at the step-2 gate.

## The three tiers

- **None (tier 1).** Workspace only. No outside sources.
- **Web (tier 2).** The AI searches the web alone, no fan-out.
- **Deep (tier 3).** The AI proposes 3 to 5 specific questions plus its Beyond-the-ask items, the user signs them off, a fan-out of sub-agents answers them (or the AI works them in sequence without sub-agents), and the result is a dated brief.

Research is sized to the build: full research only when the build warrants it. The feedback loop checks every run for too much or too little.

**Sources at deep. The AI picks, or the user names one:**
- The web: the default.
- A book: the AI proposes it; if the build warrants it, a pack-building tool digests it into reusable knowledge (that work belongs to the tool at step 6, not this step).
- Video, audio, podcasts: a transcription tool, one job at a time on a shared CPU.
- What people are saying right now: a recent-discussion search across forums and social platforms, when the field moves monthly.
- Existing skills and repos: a skills registry plus a GitHub search; this is already the outside sweep.
- Official docs: a docs-lookup tool, for technical builds only.
- A person: a peer, a partner, a friend who has done it. The AI drafts the question, the user asks. Cheapest first-hand source there is.

Where the brief lives: tier 3 in the build's `research/` folder; tier 2 in the same STATUS that holds the Define and plan.

## Both sweeps, every time, inside then outside

**Inside the workspace.** Check the user's existing skills, templates and past builds for something that already solves this. Surface what exists before proposing anything new.

**Outside the workspace, per mechanic, not per domain.** For each mechanic on the run card, three lookups in order, stop at the first that holds:
1. **Already installed.** `python3 -c "import x"`, `npm ls`, the AI's skills folder, the workspace's tools folder.
2. **A skills registry.** For example `npx skills find "<mechanic>"`; open the top hits, registries print little description.
3. **GitHub.** One search for the mechanic by name (`gh search repos "<mechanic>"`); a known URL is read through a plain page fetcher.

Every tier runs all three on each mechanic the mode sweeps; tier 3 may fan them out. Knowledge mode sweeps only mechanics that are scripts or repeatable structures. Verdict per mechanic: whole / part / spark / **build it**.

Why this rule exists: a YAML frontmatter parser was hand-rolled twice in one workspace, with a YAML library installed the whole time, and one of the two had a bug that false-failed more than half the files it checked. The earlier search had been for "skill builder", never "frontmatter parser".

**Guardrail on both:** hits go into the brief as candidates; nothing is read into the build chat unless the plan names that part.

## Source rule

- Lead with the first-hand reason (what happened in this workspace, what the user did or said). Put borrowed sources after, if at all.
- A source counts only if the recommendation would flip if the source said the opposite. Otherwise leave it out.
- Say in one clause *why* a source transfers to the case at hand (a book for surgeons is not authority on AI design).
- Numbers come from a shown count or are labelled a guess.

## Whole / part / spark / build it

The verdict on any existing skill, pack, or convention the sweep turns up, and why it serves the goal:

- **Whole.** The entire piece, by reference, unchanged. Example: the user's existing project-folder convention.
- **Part.** A named piece is lifted, nothing else. Example: one gate prompt from an older process; the rest retired.
- **Spark.** The idea informs the design; nothing is read in.
- **Build it.** Nothing fit; the brief names what was searched so the next build does not search again.

Only the named part of a borrowed skill is read into the chat, and the plan lists every borrowed part.
