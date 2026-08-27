# learn

A Claude Code skill that turns Claude into a daily tutor. Give it a topic and it researches a curriculum from real sources, then runs ~30-minute lessons with a few exercises each. It keeps a persistent notebook of what has clicked and what is still shaky, so a course spanning months of short sessions stays coherent.

Built for learning after work: short lessons, breadth-first, intuition over grinding. The exercises are probes to check whether an idea landed, not gates you have to pass.

## Install

```bash
git clone https://github.com/derwells/learn-skill ~/.claude/skills/learn
```

That's it. Claude Code picks up skills in `~/.claude/skills/` automatically.

## Use

| Say | What happens |
|---|---|
| `/learn new bayesian statistics` | Researches and writes a full curriculum (the expensive step, done once) |
| `/learn` or "today's lesson" | Runs a ~30 min session |
| `/learn status` | Progress across your courses |
| `/learn review` | Revisits shaky ideas from fresh angles, no new material |
| `/learn curate` | No lesson; retune how the course is run |

Courses live in `.learning/` at the root of whatever project you run it in:

```
.learning/
├── learner.md             # what the tutor knows about you, across all courses
└── <course>/
    ├── curriculum.md      # units, lessons, and the intuition each one must land
    ├── progress.json      # the tutor's notebook: what clicked, what's shaky, why
    ├── materials/         # researched teaching notes per unit
    └── sessions/          # short log per session
```

Commit `.learning/` if the project is a repo. Your learning history is worth versioning.

## How it teaches

- Anchors every concept with an analogy before formalizing it
- Checks understanding by making you produce something: explain it back, predict an outcome, spot the bug in a broken version
- Never reuses a problem or framing you've already seen
- Follows your "wait, why?" questions at the expense of coverage
- Records its own mistakes at the end of each session and reads them before the next one

Most of what's in `SKILL.md` was earned through real sessions rather than designed up front. The rules in it exist because their absence broke something at least once.

## License

MIT
