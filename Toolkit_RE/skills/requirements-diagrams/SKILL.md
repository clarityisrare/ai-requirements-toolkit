---
name: requirements-diagrams
description: >-
  Creates Mermaid diagrams for requirements and specs at any stage of the
  requirements workflow: a system context diagram, a use-case overview, a
  request/approval state machine, a sequence diagram, or a requirements-to-test
  traceability graph — tailored to the user's
  system and ready to drop into a Markdown spec (GitHub renders them as-is).
  Triggers whenever a user says things like "draw a context diagram", "diagram
  this approval flow", "show the states a request goes through", "sequence
  diagram for the upload", "map the actors and use cases", "visualise how
  requirements trace to tests", or "give me a Mermaid diagram for this spec".
  For requirements and spec diagrams specifically — not general code, class, or
  database-schema diagrams. Outputs Mermaid (.mmd) that
  renders on mermaid.live, in GitHub Markdown, or any Mermaid-aware tool.
model: opus # Skill is model-agnostic and runs on other LLMs; pinned to opus for the intended experience.
---

# Requirements Diagrams

A diagram often communicates a requirement faster than a paragraph. This skill
produces clean Mermaid diagrams tailored to the user's system, using six proven
starting points as reference — so the result is a real, renderable diagram, not a
sketch.

Each reference in `references/diagrams/` is a worked Mermaid example. Read the one
that matches, learn its structure, then rebuild it around the user's actors,
states, and steps — never just relabel the sample's nodes, because a relabeled
sample still describes the reference system, not the user's, and misleads whoever
reads the spec. For a spec description turned into a diagram, with the changes from
the sample called out, see
[`references/worked-example.md`](references/worked-example.md).

## Choosing the diagram

| The user wants to show… | Diagram type | Reference |
|---|---|---|
| The system and everything around it (actors, externals) | Context | `references/diagrams/context-diagram.mmd` |
| Which actors perform which use cases | Use-case overview | `references/diagrams/use-case-overview.mmd` |
| The states a request/record moves through | State machine | `references/diagrams/request-lifecycle-state.mmd` |
| An approval / sign-off flow | Flow | `references/diagrams/approval-process.mmd` |
| The step-by-step interaction between parts | Sequence | `references/diagrams/upload-sequence.mmd` |
| How requirements link to stories and tests | Traceability graph | `references/diagrams/requirements-traceability.mmd` |

**State machine vs Flow** cover the same request/approval lifecycle from two
angles: a state machine shows what a record *is* at each point (its status), a flow
shows what actors *do* to move it along. Reach for the state machine when the
question is "what status is it in", the flow when it is "who does what next".

If the user is not sure which they need, ask what they are trying to communicate
and to whom — a context diagram for stakeholders, a state machine for developers,
a sequence for an integration.

## Workflow

1. **Gather the specifics.** Actors, system boundary, the states or steps, the
   trigger and end conditions. Do not invent parts of the system the user has not
   described; ask instead, because a fabricated actor or state becomes a
   requirement nobody agreed to.
2. **Pick and read the matching reference** for correct Mermaid syntax and a sound
   structure.
3. **Rebuild it for their system.** Replace every node, actor, and transition with
   the user's real ones. Keep it readable — prune nodes that do not earn their
   place, because a diagram that tries to show everything shows nothing.
4. **Verify it renders.** When mermaid-cli is available, run
   `npx -y @mermaid-js/mermaid-cli -i diagram.mmd -o /dev/null` and fix what it
   reports. Otherwise check the diagram against
   [`references/mermaid-pitfalls.md`](references/mermaid-pitfalls.md). State in your
   reply whether the diagram was machine-verified or only reviewed.
5. **Return the diagram.** Return it inline in a ```mermaid fenced block so it
   renders directly in Markdown, on mermaid.live, and in GitHub. Write a `.mmd`
   file only when the user asks for a file or names a path.
6. **Offer refinements** — a second view (e.g. a state machine to complement a
   sequence) if it would clarify the spec.

## Principles

- **Match the diagram to the audience.** The same feature warrants different views
  for stakeholders, developers, and testers.
- **Model what exists, ask about what does not.** Do not fabricate system parts to
  fill the picture, because an invented component misrepresents the system the team
  has to build.
- **Readable beats complete.** Fewer, well-chosen nodes communicate more.
- **Always renderable.** Hand back valid Mermaid the user can paste and see, and
  verify it (step 4) rather than assuming it parses.
- **Minimal prose.** Return the diagram with a brief note on what it shows; do not
  wrap it in long narration or restate the whole system in text, because the diagram
  is the deliverable and prose that repeats it buries what the user asked for.
