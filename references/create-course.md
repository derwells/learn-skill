# Mode: Create a course


This is the expensive step — do it once, thoroughly, so every future session is instant.

1. **Scope interview (brief).** Ask only what you can't infer: their current level with the topic, what they want to be able to *do or understand* at the end, any deadline, and **how they want it run — drilled like a student (`tutor`) or briefed like a colleague (`design-partner`)**. One round of questions, not an interrogation. Before researching, check `.learning/` for existing courses whose goals overlap the new one; propose merging or a companion structure instead of a silent parallel course, and read `learner.md` so day one inherits everything already known about the learner.

2. **Research deeply.** This can take a while and that's expected — the whole point of persisting materials is to never pay this cost twice. Use web search for current best references, syllabi from real university courses, canonical textbooks, and the best explanations and analogies people have found for the hard ideas. If a cheap parallel-research facility is available (a research skill, subagents on a smaller model), fan out the broad gathering (e.g., one query per candidate unit) and keep your own context for synthesis. You are building the course from real sources, not just from memory — memory gets the shape right but misses the best explanations and modern practice.

3. **Write `curriculum.md`.** Structure: course goal → total hour estimate (state it honestly; 500 hours is a fine answer) → units → lessons. Each **lesson** is sized for roughly one session (~30 min) and lists: the concepts it introduces (with stable concept IDs like `stats.clt`), prerequisites, and its **key intuition** — a one-line statement of the thing that must click (e.g., "the CLT is about *sums* washing out the shape of the parts — see why averaging is summing"). Number units and lessons.

4. **Write `materials/unit-NN-<slug>.md` for at least the first two units** — teaching notes: the core ideas explained well, the best available analogies, worked examples, a pool of exercise seeds per lesson (probes, not quizzes), common misconceptions, and source links. Later units can be researched lazily when the user is one unit away from reaching them (do this at the *end* of a session so it never delays one).

5. **Initialize `progress.json`** and tell the user the shape of the course: total estimated hours, number of units, and what session 1 will cover. Do not run a session in the same sitting unless they ask.

