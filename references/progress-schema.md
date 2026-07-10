# progress.json — the tutor's notebook

`progress.json` is the persistent memory that keeps a months-long course coherent. It is a *notebook*, not a scorecard: its job is to let a future session pick up exactly where understanding actually is — which ideas have clicked, which are still shaky and *why*, and which explanations worked — without the user having to re-explain themselves.

Read it at the start of every session; write it at the end (and after any notable event mid-session if the conversation might get cut off).

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
  This is a judgment formed from the whole conversation — explanations in the user's own words, questions they ask, reasoning on probes, and their own self-report — not a count of exercise results. Move it in either direction whenever the evidence says so.
- **`notes`** (per concept) is the heart of the notebook: live misconceptions stated precisely, which analogies/explanations landed, and what angle to try next. Short entries; keep the 3–4 most useful, prune stale ones when a misconception dies.
- **`seen_angles`** stores one-line fingerprints (session + gist) of problems and framings already used, so revisits are never reruns. Cap at ~5 per concept, oldest dropped.
- **`notes`** (top level) is free-form tutor memory: learning-style observations, pacing preferences, recurring struggles, how the user likes the course run. Update sparingly; read always.

## Choosing warm-up items

No scheduling algorithm — pick by judgment at session start: shaky concepts first (freshest misconception first), then any settling concept that hasn't been touched in a while or that today's lesson will build on. Cap at 2–3; this is a course, not a card deck. If shaky items pile up faster than warm-ups can absorb (more than ~6), suggest a `/learn review` session rather than crowding regular sessions.

## Streak

Increment `streak.current` if the last session was yesterday or today; reset to 1 otherwise. Never guilt the user about a broken streak — note the new one starting and move on.
