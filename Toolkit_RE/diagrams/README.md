# Requirement & spec diagrams

Six worked Mermaid starting points for requirements and specs. Copy one, then
rebuild it around your own actors, states, and steps.

| File | Shows |
|---|---|
| `context-diagram.mmd` | The system and everything around it (actors, externals) |
| `use-case-overview.mmd` | Which actors perform which use cases |
| `request-lifecycle-state.mmd` | The states a record moves through (its status) |
| `approval-process.mmd` | An approval / sign-off flow (who does what next) |
| `upload-sequence.mmd` | The step-by-step interaction between parts |
| `requirements-traceability.mmd` | How requirements link to stories and tests |

## Kept in sync with the skill bundle

These six files are mirrored, byte-for-byte, into
`skills/requirements-diagrams/references/diagrams/`, because each shipped skill has
to be self-contained (see [`skills/README.md`](../skills/README.md)). There is no
build step that regenerates one from the other, so an edit to either copy must be
copied across by hand or the two silently drift apart.

Verify the two copies still match:

```bash
diff -r --exclude=README.md diagrams skills/requirements-diagrams/references/diagrams
```

No output means they are in sync. Any output lists the files that have drifted.
