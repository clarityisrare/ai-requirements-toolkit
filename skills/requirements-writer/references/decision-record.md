# Decision Record

A lightweight record of a significant decision — why it was made, and what was traded away.
Also called an ADR (Architecture Decision Record). Keep one file per decision; never rewrite
history — supersede an old record with a new one.

---

## ID

DR-001

---

## Title

Restrict document uploads to PDF only

---

## Status

Proposed / Accepted / Superseded by DR-XXX / Rejected

---

## Date

2026-05-20

---

## Context

What is the situation and the forces at play? What problem or question prompted this
decision? Include relevant constraints, assumptions, and stakeholders.

---

## Decision

What did we decide? State it in one clear sentence, then any necessary detail.

> We will accept only PDF uploads for supporting evidence in the first release.

---

## Alternatives Considered

| Option | Pros | Cons | Why not chosen |
|---|---|---|---|
| Allow PDF + images | Broader input | More validation, more scanning surface | Deferred to a later release |
| Allow any file type | Maximum flexibility | High security and storage risk | Rejected |

---

## Consequences

- What becomes easier or harder as a result?
- What follow-up work or new requirements does this create?
- What risks are we accepting?

---

## Links

- Related requirements: REQ-001
- Related decisions: —
