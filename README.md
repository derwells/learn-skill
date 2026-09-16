# learn

Claude Code skill that turns Claude into a daily tutor. Give it a topic, it researches a curriculum, then runs short lessons in dialogue, with code and figures in Jupyter notebooks. Keeps a notebook of what clicked and what didn't, so a course survives months of short sessions.

I made this because I couldn't study consistently after work. Textbook exercises want a full hour of deep focus and I never had that at 9pm. These lessons are short enough to do tired. The tutor remembers where you left off, you just show up.

## Install

Works with any harness that supports [Agent Skills](https://agentskills.io) (Claude Code, opencode, Codex, Gemini CLI, ...). Clone into your harness's skills directory:

```bash
# Claude Code (opencode reads this path too)
git clone https://github.com/derwells/learn-skill ~/.claude/skills/learn

# Codex and others
git clone https://github.com/derwells/learn-skill ~/.agents/skills/learn
```

Needs web search (curriculum research), `jq` or `python3` (notebook validation), and Jupyter via `uv` for lesson notebooks.

## Use

| Say | What happens |
|---|---|
| `/learn new bayesian statistics` | Researches and writes the curriculum. Expensive, done once |
| `/learn` or "today's lesson" | ~30 min session |
| `/learn status` | Progress across courses |
| `/learn review` | Revisit shaky ideas, no new material |
| `/learn curate` | No lesson. Retune how the course is run |

Courses live in `.learning/` at the project root:

```
.learning/
├── learner.md             # what the tutor knows about you, across courses
└── <course>/
    ├── curriculum.md      # units, lessons, the intuition each one must land
    ├── progress.json      # tutor's notebook: what clicked, what's shaky, why
    ├── materials/         # teaching notes per unit, one vetted example per idea
    ├── notebooks/         # one Jupyter notebook per lesson
    └── sessions/          # short log per session
```

Worth committing `.learning/` if the project is a repo.

## How it teaches

- Fitting examples first, then the math. The smallest real case where you can see the whole mechanism, or an analogy whose mapping is spelled out. Never a random example
- Explains, then stops. Lets the idea sit and takes the next step from what you say, instead of quizzing you the moment it finishes a paragraph
- Probes instead of quizzes, and later rather than sooner: predict what a cell prints, pick the right prior, spot what's wrong in a broken version
- Code and figures in a Jupyter notebook per lesson, executed before it points you at a cell
- Never repeats a problem or framing you've already seen
- Your questions > coverage. 30 minutes is a guideline, not a pace
- Logs its own mistakes at session end, reads them next session

Wrong answers are fine. What matters is you end up seeing why.

A concept entry in the notebook looks like this:

```json
"stats.clt": {
  "understanding": "settling",
  "notes": [
    "clicked via the 'many small independent nudges' framing",
    "still conflates convergence of the distribution with a sample path — try a simulation angle next"
  ]
}
```

That's what the tutor reads back three weeks later. It never re-asks a question you've seen — it tracks the angles it has already tried.

Most of SKILL.md came from real sessions, not upfront design. Almost every rule in it is there because not having it broke a session at least once.

## License

MIT
