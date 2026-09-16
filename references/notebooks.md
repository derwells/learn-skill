# Lesson notebooks

Code and figures live in Jupyter notebooks, one per lesson, at
`.learning/<course>/notebooks/<unit>-<lesson>-<slug>.ipynb`. The learner opens the notebook
(VS Code, JupyterLab, or a browser over SSH) beside the chat. The chat carries the dialogue;
the notebook carries everything runnable and everything visual.

A course may declare a different notebook tool in its "Course mode" section (marimo `.py`
notebooks, for instance, when the learner wants git-diffable, reactive files). Default to
Jupyter when unstated. The rules below apply either way.

## Rules

1. **Execute before you point.** Never reference a cell, output, or figure the learner can't
   already see. Run the notebook in place before mentioning it:
   `jupyter nbconvert --to notebook --execute --inplace <path>`. If a cell fails, fix it
   first — a lesson built on a broken cell derails the session.
2. **Figures are claims.** Label the axes, mark anything that must line up (a tick, a guide
   line, a label). Look at the rendered output before pointing at it and confirm it shows
   the thing you're about to say. No decorative or approximate geometry.
3. **Small cells, one idea each.** A markdown cell with the idea in plain words (the same
   sentence you'd say in chat), then a short code cell that shows it. Variable names are
   the concept's names.
4. **Predict-then-run is the canonical probe.** A markdown cell that asks for a prediction
   ("what shape does `futures` have? what happens to the fan if `num_samples=1`?"), then the
   code cell. The learner answers in chat, then runs. Ask the prediction only after the idea
   has had time to sit — the probe rules in SKILL.md apply to notebooks too.
5. **The learner types too.** Hands-on lessons leave a cell for them to complete
   (`# your turn:` with the setup written). Their cell counts as a production probe.
6. **Keep notebooks per lesson, not per session.** A revisit adds cells to the lesson's
   notebook under a dated heading; it doesn't create a new file. Cap notebooks at what one
   sitting can read.
7. **Write with the host's notebook tool** (`NotebookEdit` in Claude Code) rather than
   hand-editing `.ipynb` JSON. If none exists, generate with `nbformat` from Python.

## Toolchain

`python3 -m venv` may be broken on the learner's machine; use `uv`.

```
uv tool install jupyterlab            # once per machine
uv venv .learning/<course>/.venv       # once per course
uv pip install --python .learning/<course>/.venv/bin/python ipykernel numpy matplotlib <course packages>
.learning/<course>/.venv/bin/python -m ipykernel install --user --name <course-slug>
```

Set the notebook's kernel to `<course-slug>` so execution uses the course venv. Course-specific
pins (e.g. `arviz<1.0`) live in the course's `progress.json` notes. Add `.venv/` to
`.gitignore`; notebooks themselves are worth committing with outputs, since the outputs are
the figures the learner saw.

## Push channel

If `learner.md` says the learner is away from the notebook (mobile, end of session), push
figures over the recorded channel (e.g. Telegram) in the same turn you build them. The
notebook remains the record; the push is a convenience.
