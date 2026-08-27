# learn

A Claude Code skill that turns Claude into a daily tutor. Give it a topic and it researches a curriculum from real sources, then runs ~30 minute lessons with a few exercises each. A notebook on disk tracks what has clicked and what is still shaky, so a course can run for months of short sessions without losing the thread.

I built it because I kept failing to study after work. Textbook exercises want you to shut everything else down and think for an hour, and I could never do that consistently at 9pm. These lessons are short and light enough to do tired, and the tutor remembers exactly where your understanding left off. Showing up is the only hard part.

## Install

```bash
git clone https://github.com/derwells/learn-skill ~/.claude/skills/learn
```

Claude Code picks up anything in `~/.claude/skills/` on its own.

## Use

| Say | What happens |
|---|---|
| `/learn new bayesian statistics` | Researches and writes a full curriculum (the expensive step, done once) |
| `/learn` or "today's lesson" | Runs a ~30 min session |
| `/learn status` | Progress across your courses |
| `/learn review` | Revisits shaky ideas from fresh angles, no new material |
| `/learn curate` | No lesson. You and the tutor retune how the course is run |

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

- Analogy first, formalism after
- It checks understanding by making you produce something: explain the idea back, or spot what's wrong in a broken version
- A problem or framing you've already seen never comes back as a probe
- Your "wait, why?" questions win over coverage, every time
- At the end of a session it writes up its own mistakes, and reads them before the next one

Exercises are probes, not gates. A wrong answer followed by "oh, I see why" counts for more than a right answer produced mechanically.

Most of what's in `SKILL.md` came out of real sessions rather than upfront design. Nearly every rule in it exists because its absence broke a session at least once.

## License

MIT
