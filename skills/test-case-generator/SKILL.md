---
name: test-case-generator
description: >-
  Use to turn a requirement and its acceptance criteria into concrete,
  executable test cases QA can run, and to link requirements → stories → tests
  in a traceability matrix so nothing ships untested. Trigger whenever a user
  says things like "write test cases for this requirement / story", "turn these
  acceptance criteria into tests", "what should QA test here?", "give me
  positive and negative test cases", "build a traceability matrix", or "how do I
  prove every requirement is covered by a test?". This is the step after
  acceptance criteria exist (see requirements-writer) — it produces the QA-facing
  artifacts and the coverage links.
model: opus
---

# Test Case Generator

Acceptance criteria describe the behaviour; test cases prove it. This skill turns
a requirement and its Given/When/Then criteria into test cases a QA engineer can
execute, and ties each one back to the requirement it verifies so coverage is
visible rather than assumed.

It works best *after* acceptance criteria exist — if they don't yet, draft them
first with the **requirements-writer** skill.

## Workflow

### Step 1 — Gather the source

Ask for:

- The requirement(s) under test.
- The acceptance criteria (Given/When/Then). If they're missing or thin, say so —
  test cases are only as good as the criteria beneath them.
- Any IDs already in use (REQ, story, AC IDs) so tests can trace back cleanly.
- The environment or data constraints QA should assume.

### Step 2 — Generate the test cases

Read `references/test-case-generator.md` and apply it as the author (don't paste
the raw prompt at the user). For each acceptance criterion, produce test cases
covering:

- Happy path.
- Negative / error scenarios.
- Boundary conditions.
- Permission / role-based scenarios where relevant.
- Data validation.

Each test case should carry an ID, a clear title, preconditions, steps, expected
result, and the **requirement / AC it verifies**. Don't invent behaviour the
criteria don't state — where a case can't be pinned to a criterion, flag the gap;
it usually means a missing acceptance criterion.

### Step 3 — Build the traceability

Populate `references/traceability-matrix.md` linking requirement → story → test
case, so every requirement maps to at least one test and every test maps back to a
requirement. Call out both kinds of gap explicitly:

- A requirement with **no test** → a coverage hole.
- A test with **no requirement** → scope creep or a missing requirement.

For a visual of the linkage, `references/requirements-traceability.mmd` is a
Mermaid diagram you can adapt and drop into a spec.

### Step 4 — Hand back with the gaps named

Return the test cases plus the matrix, and lead with any coverage gaps found —
those are the most valuable output, because they're what would otherwise ship
untested.

## Principles

- **Every test traces back.** A test that verifies nothing, or a requirement no
  test touches, is the finding — surface it.
- **Cases come from criteria.** Don't invent behaviour; if a needed test has no
  criterion, that's a gap for requirements-writer to close.
- **QA-executable.** Preconditions, steps, and expected results concrete enough to
  run without guessing.
