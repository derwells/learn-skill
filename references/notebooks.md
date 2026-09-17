# Lesson notebooks

Substantial runnable demonstrations and persistent figures live in Jupyter notebooks, one per lesson, at
`.learning/<course>/notebooks/<unit>-<lesson>-<slug>.ipynb`. The learner opens the notebook
(VS Code, JupyterLab, or a browser over SSH) beside the chat. Short inline code and equations
can support the dialogue without creating a notebook. Use a notebook when execution, a figure,
or continued experimentation helps the lesson; do not interrupt an explanation to satisfy a format.

A course may declare a different notebook tool in its "Course mode" section (marimo `.py`
notebooks, for instance, when the learner wants git-diffable, reactive files). Default to
Jupyter when unstated. The rules below apply either way.

## Rules

1. **Execute demonstrations before you point.** Run completed demonstration cells and
   inspect their outputs before referring to them. For a notebook containing only completed
   demonstrations, use `jupyter nbconvert --to notebook --execute --inplace <path>`.
   Keep unfinished exercises and answers to pending predictions out of bulk execution.
   Validate prediction results in a separate scratch execution, without publishing the answer
   in the learner's notebook. A failed demonstration must be repaired before teaching from it.
2. **Figures are claims.** Label the axes, mark anything that must line up (a tick, a guide
   line, a label). Look at the rendered output before pointing at it and confirm it shows
   the thing you're about to say. No decorative or approximate geometry.
3. **Make the argument visible.** Introduce the lesson's question, explain why each code
   step is needed, and connect the output to the general claim. Keep cells small enough to
   inspect. Use consistent variable names across chat, code, and figures.
4. **Compare deliberately.** Where a distinction matters, show cases with the same setup
   and change the relevant feature. Align plots and scales where comparison requires it.
   Explain what changed and why. A prediction before execution is useful when the learner
   has enough information to reason; explain first when they do not.
5. **Reduce help as appropriate.** A worked example can lead to a partly completed cell
   and then a new application. Leave consequential decisions to the learner, with setup
   supplied. Participation follows the course mode and the learner's preference. A notebook
   walkthrough is valid when they want to listen; missing exercise answers are not failures.
6. **Keep notebooks per lesson, not per session.** A revisit adds cells to the lesson's
   notebook under a dated heading; it doesn't create a new file. Use sections so a lesson
   spanning sessions remains navigable.
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

If the learner is away from the notebook, use an available delivery method they have
authorized under the host's rules. A recorded channel preference alone does not override
the host's permission requirements. The notebook remains the record. If external sending
is unavailable, show the figure in the current interface when possible.
