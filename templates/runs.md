# rome: runs (append-only, one row per build, written by the feedback loop)

| date | tier | summary | corrections | signal |
|---|---|---|---|---|
| YYYY-MM-DD | T<n> | <locked goal, verbatim> · <where the built thing lives, by path> · <how the eight steps went, where it retired> | <what the user corrected, comma-separated slugs, or "none"> | y / n (did the run produce something the user will act on) |

# rome: review log (one row per second-reviewer pass)

| date | build | step | what the reviewer caught | what it missed | minutes | worth it |
|---|---|---|---|---|---|---|
| YYYY-MM-DD | <build> | 5 / 7 | <n findings, m real: the one that mattered> | <what the user's own read found that it did not> | <n> | y / n |

The autonomy ladder (optional): once a decision the AI makes on its own has gone three runs without a correction, it stops being asked and starts being printed. Track those here:

| decision | rung | clean runs | note |
|---|---|---|---|
| fill the six intake variables | prints, user corrects | 0/3 | starts here by SKILL.md § 1; a run where the user corrected two or more variables resets the count |
| pick the research sources at step 2 | asks | 0/3 | promote to "prints, user corrects" after three clean runs |
| rule an open decision by the stated lean when the user says "approve" without naming it | asks | 0/3 | |
