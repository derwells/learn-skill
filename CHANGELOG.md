# Changelog

## 1.0.0 — 2026-09-01

First public release.

- Intuition-first tutoring: analogies and dialogue first, exercises as probes rather than gates
- Persistent tutor notebook (`progress.json`) plus a cross-course learner profile (`learner.md`)
- Write integrity rules: mid-session checkpoints, JSON validated after every write
- Modes: `new`, session (default), `review`, `status`, `curate`
- Two course styles: `tutor` (probed) and `design-partner` (briefed)
- Course contract: earned, numbered rules read first every session
- Freshness policy for fast-moving topics, with lazy per-unit research
- Mode playbooks split into `references/` so sessions load only what they need
- Frontmatter kept to the Agent Skills open-spec fields — portable across Claude Code, opencode, Codex, Gemini CLI
