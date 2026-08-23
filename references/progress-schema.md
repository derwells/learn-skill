# progress.json — the tutor's notebook

`progress.json` is the persistent memory that keeps a months-long course coherent. It is a *notebook*, not a scorecard: its job is to let a future session pick up exactly where understanding actually is — which ideas have clicked, which are still shaky and *why*, and which explanations worked — without the user having to re-explain themselves.

It records **the learner, not the subject** — the tutor already knows the material, so explanations, definitions, and content summaries never belong here. And it records **judgments, not history**: a future session brings the same judgment you have now and can re-derive anything derivable from a current assessment plus the curriculum. So write down only what can't be re-derived: the current understanding level, live misconceptions stated precisely in the learner's terms, pointers to the framings that landed (name the analogy, don't re-explain it), and what to try next. What happened session by session belongs in `sessions/*.md` — if a concept's notes read like a chronicle ("s4 delivered X… s5 broke… s6 landed") or like a textbook, they're duplicating something the next session already has and should be collapsed.

Read it at the start of every session (after `.learning/learner.md`, the cross-course profile). Don't wait for the close to write it: checkpoint at every natural boundary — a lesson closing, any course-run feedback from the user (same turn, always), the ~30-minute mark — and finish the write at the close. After **every** write, parse the file back (`jq empty` or equivalent): a corrupt notebook silently loses weeks of judgment, and JSON's duplicate keys don't error — they shadow earlier entries, so when adding to `concepts` or `seen_angles`, extend the existing key's array rather than re-adding the key.

```json
{
  "course": "statistics",
  "created": "2026-07-10",
  "estimated_total_hours": 120,
  "hours_logged": 14.5,
  "sessions_completed": 27,
  "streak": { "current": 5, "best": 12, "last_session_date": "2026-07-09" },
  "current": { "unit": 3, "lesson": "3.2" },
  "lessons": {
    "1.1": { "status": "complete", "sessions_spent": 1, "completed_on": "2026-06-12" },
    "3.2": { "status": "in_progress", "sessions_spent": 2 }
  },
  "concepts": {
    "stats.clt": {
      "name": "Central Limit Theorem",
      "lesson": "2.3",
      "understanding": "settling",
      "last_touched_session": 24,
      "notes": [
        "clicked via the 'many small independent nudges' framing; the galton board analogy landed",
        "still conflates convergence of the distribution with convergence of a sample path — revisit with a simulation angle"
      ]
    }
  },
  "seen_angles": {
    "stats.clt": [
      "s24: galton board analogy + derive sampling dist of mean for exp(λ)",
      "s19: predict-output numpy simulation"
    ]
  },
  "notes": "Prefers code-first sessions; analogies land well; shaky on measure-theoretic language, avoid it."
}
```

Field notes:

- **`concepts`** is keyed by the stable concept IDs defined in `curriculum.md`. Concepts are the unit of understanding; lessons are just the delivery order.
- **`understanding`** is the tutor's judgment of how settled the intuition is, one of three values:
  - `"shaky"` — taught, but it hasn't clicked; the user can't yet say why it works. Revisit from a *different angle* within a session or two.
  - `"settling"` — clicked with scaffolding, or clicked once but hasn't been used since. Weave it into later material where it naturally recurs; spot-check in a warm-up.
  - `"solid"` — the user can explain why it works and where it breaks, and has followed it in a fresh context. Occasional spot-checks only.
  This is a judgment formed from the whole conversation — explanations in the user's own words, questions they ask, reasoning on probes, and their own self-report — not a count of exercise results. Move it in either direction whenever the evidence says so. **Floor: a concept the user never engaged with (delivered, but never explained back, applied, or questioned) stays `"shaky"` regardless of how the delivery went; promotion requires a successful fresh-angle probe, ideally in a later session.**
- **`notes`** (per concept) is the heart of the notebook: live misconceptions stated precisely, which analogies/explanations landed, and what angle to try next. Short entries; keep the 3–4 most useful, prune stale ones when a misconception dies. **When a lesson closes, compact its concepts' notes to the durable residue** — state, keeper framings, open spot-checks — and drop the narrative (it lives in the session logs).
- **`seen_angles`** stores one-line fingerprints (session + gist) of problems and framings already used, so revisits are never reruns. Cap at ~5 per concept, oldest dropped.
- **`notes`** (top level) is free-form tutor memory — but only for what's *course-specific*: how this course is run, its goals and grounding, environment recipes it alone needs. If the course has a **contract** (see SKILL.md), it sits at the top of this field, numbered, and is read before everything else. Anything true of the learner in every course (environment, energy patterns, math background, analogy rules, probe craft) belongs in `.learning/learner.md`, not here — never duplicate it. Update sparingly; read always.

Optional fields that mature courses have found useful (add them when the course needs them, in this shape):

- **`status`** (course-level): `"active"` (default when absent), `"paused"`, or `"archived"` — set from an explicit decision with the user (usually via `/learn status` flagging dormancy). Include a one-line note saying why and what would reactivate it. Paused/archived courses are skipped by session mode.
- **`glossary`** — for courses with a fluency goal: term → where the learner met it + state + any learner-specific hook. Never a re-teaching (generate glosses fresh at drill time); prune entries that go solid.
- **`next_session`** — a few lines of pointers for the next session's tutor: what to open with and why, decisions pending. Pointers, not a script: cap at roughly ten lines, rewrite it whole at each close (never append), and keep judgments out of it — they live in `concepts`.

## Choosing warm-up items

No scheduling algorithm — pick by judgment at session start: shaky concepts first (freshest misconception first), then any settling concept that hasn't been touched in a while or that today's lesson will build on. Cap at 2–3; this is a course, not a card deck. If shaky items pile up faster than warm-ups can absorb (more than ~6), suggest a `/learn review` session rather than crowding regular sessions.

## Streak

Increment `streak.current` if the last session was yesterday or today; reset to 1 otherwise. Never guilt the user about a broken streak — note the new one starting and move on.
