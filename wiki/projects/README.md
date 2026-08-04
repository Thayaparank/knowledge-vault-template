# wiki/projects/ — Per-Project Files

Each active project gets up to four files (templates in `../../templates/`):

| File | Holds |
|---|---|
| `<project>.md` | Hub: background, key facts, links — stable, changes rarely |
| `<project>-status.md` | Current state only, topped by `NEXT ← RESUME HERE` |
| `<project>-decisions.md` | Numbered decisions: locked / open / rejected, each dated |
| `<project>-changelog.md` | Append-only dated history |

The test: someone who has never seen the project reads the status file and can continue the work with zero questions.
