---
name: requirements-diagrams
description: >-
  Use to create Mermaid diagrams for requirements and specs — a system context
  diagram, a use-case overview, a request/approval state machine, a sequence
  diagram, or a requirements-to-test traceability graph — tailored to the user's
  system and ready to drop into a Markdown spec (GitHub renders them as-is).
  Trigger whenever a user says things like "draw a context diagram", "diagram
  this approval flow", "show the states a request goes through", "sequence
  diagram for the upload", "map the actors and use cases", "visualise how
  requirements trace to tests", or "give me a Mermaid diagram for this spec".
  For requirements and spec diagrams specifically — not general code, class, or
  database-schema diagrams. Useful at any stage of the requirements lifecycle.
  Outputs Mermaid (.mmd) that
  renders on mermaid.live, in GitHub Markdown, or any Mermaid-aware tool.
model: opus
---

# Requirements Diagrams

A diagram often communicates a requirement faster than a paragraph. This skill
produces clean Mermaid diagrams tailored to the user's system, using six proven
starting points as reference — so the result is a real, renderable diagram, not a
sketch.

Each reference in `references/diagrams/` is a worked Mermaid example. Read the one
that matches, learn its structure, then rebuild it around the user's actors,
states, and steps — never just rename the sample's labels.

## Choosing the diagram

| The user wants to show… | Diagram type | Reference |
|---|---|---|
| The system and everything around it (actors, externals) | Context | `references/diagrams/context-diagram.mmd` |
| Which actors perform which use cases | Use-case overview | `references/diagrams/use-case-overview.mmd` |
| The states a request/record moves through | State machine | `references/diagrams/request-lifecycle-state.mmd` |
| An approval / sign-off flow | Flow | `references/diagrams/approval-process.mmd` |
| The step-by-step interaction between parts | Sequence | `references/diagrams/upload-sequence.mmd` |
| How requirements link to stories and tests | Traceability graph | `references/diagrams/requirements-traceability.mmd` |

If the user isn't sure which they need, ask what they're trying to communicate
and to whom — a context diagram for stakeholders, a state machine for developers,
a sequence for an integration.

## Workflow

1. **Gather the specifics.** Actors, system boundary, the states or steps, the
   trigger and end conditions. Don't invent parts of the system the user hasn't
   described — ask.
2. **Pick and read the matching reference** for correct Mermaid syntax and a sound
   structure.
3. **Rebuild it for their system.** Replace every node, actor, and transition with
   the user's real ones. Keep it readable — prune nodes that don't earn their
   place; a diagram that tries to show everything shows nothing.
4. **Return renderable Mermaid.** Provide the `.mmd` source and, when it helps,
   wrap it in a ```mermaid fenced block so it renders directly in Markdown. Note
   that it renders as-is on mermaid.live and in GitHub.
5. **Offer refinements** — a second view (e.g. a state machine to complement a
   sequence) if it would clarify the spec.

## Principles

- **Match the diagram to the audience.** The same feature warrants different views
  for stakeholders, developers, and testers.
- **Model what exists, ask about what doesn't.** Don't fabricate system parts to
  fill the picture.
- **Readable beats complete.** Fewer, well-chosen nodes communicate more.
- **Always renderable.** Hand back valid Mermaid the user can paste and see.
