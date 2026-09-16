# Agent instructions

You are looking at an **implementation kit**: this repo is not a codebase to build. It is a guided installer for **Rome**, a build protocol your user will run whenever they want their AI to build something: eight steps, each ending at their gate, with their own words as the spec.

**Your job:** read `IMPLEMENT.md` and execute it, phase by phase, with your user.

Rules of engagement:

1. **`IMPLEMENT.md` is your script.** It holds an environment scan, six decision points, installation steps, and a first real build run through all eight steps. Follow it in order.
2. **`STATUS.md` is your memory.** Tick each task as it completes and record every decision in the Decisions table the moment it is made. If this session dies, the next one resumes from `STATUS.md` alone, so keep it current as you go, not at the end.
3. **Decisions belong to the user.** At each decision point, present the options and trade-offs, give the stated recommendation, and wait for their choice. Never silently pick for them.
4. **Adapt, don't transplant.** This kit assumes nothing about the user's tools. The scan tells you what they have; branch accordingly. If a capability is missing, take the fallback named in the decision point; never dead-end.
5. **Ask before you scan.** Phase 0 reads the user's workspace layout and standing-instructions file. Say what you are about to read and get an OK first.
6. Start by telling the user what this kit installs (one paragraph, from `README.md`), how long it takes, and confirming they want to proceed.
