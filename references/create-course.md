# Mode: Create a course


This is the expensive step — do it once, thoroughly, so every future session is instant.

1. **Scope interview (brief).** Ask only what you can't infer: their current level with the topic, what they want to be able to *do or understand* at the end, any deadline, and **how they want it run — drilled like a student (`tutor`) or briefed like a colleague (`design-partner`)**. One round of questions, not an interrogation. Before researching, check `.learning/` for existing courses whose goals overlap the new one; propose merging or a companion structure instead of a silent parallel course, and read `learner.md` so day one inherits everything already known about the learner.

2. **Research deeply.** This can take a while and that's expected — the whole point of persisting materials is to never pay this cost twice. Use web search for current best references, syllabi from real university courses, canonical textbooks, and the best explanations and analogies people have found for the hard ideas. If a cheap parallel-research facility is available (a research skill, subagents on a smaller model), fan out the broad gathering (e.g., one query per candidate unit) and keep your own context for synthesis. You are building the course from real sources, not just from memory — memory gets the shape right but misses the best explanations and modern practice.

3. **Write `curriculum.md`.** Structure: course goal → total hour estimate (state it honestly; 500 hours is a fine answer) → units → lessons. Each **lesson** is sized for roughly one session (~30 min) and lists: the concepts it introduces (with stable concept IDs like `stats.clt`), prerequisites, and its **key intuition** — a one-line statement of the thing that must click (e.g., "the CLT is about *sums* washing out the shape of the parts — see why averaging is summing"). Number units and lessons.

4. **Write `materials/unit-NN-<slug>.md` for at least the first two units.** Teaching notes, organised by key intuition. For each key intuition:
   - **One canonical example**, chosen with the fit test from SKILL.md ("The explanation standard"): the minimal real instance where the whole mechanism is visible, or an analogy whose map you can write and whose breaking point you can name. Find who explains this idea best (a lecturer, a textbook, a blog post people keep linking) and what example *they* use; steal it, cite it. This is the moment to be picky — the session can't be.
   - The plain-words statement and the exact statement, side by side, checked to be the same claim.
   - The one figure that shows it (what's on each axis), as a matplotlib sketch or a description precise enough to draw from.
   - The actual math, in the order analogy → formula → real numbers through it once.
   - Common misconceptions, stated as the learner would say them.
   - A few probe seeds (predict / pick / write), for use *after* the idea has sat.
   - Source links.
   Later units are researched lazily when the user is one unit away (at the *end* of a session, so it never delays one).

4b. **Scaffold the first lesson's notebook** (`notebooks/`, see `references/notebooks.md`): the canonical example as runnable cells with the figure, executed so outputs exist. Later lesson notebooks are built at the end of the session before they're needed.

5. **Initialize `progress.json`** and tell the user the shape of the course: total estimated hours, number of units, and what session 1 will cover. Do not run a session in the same sitting unless they ask.

