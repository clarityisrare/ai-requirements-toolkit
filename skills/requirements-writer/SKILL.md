---
name: requirements-writer
description: >-
  Use to DRAFT requirements once you understand what the business needs — the
  step after elicitation. Turn a feature idea, a business request, or notes from
  a discovery workshop into clear, testable, traceable requirements: functional
  requirements, INVEST user stories, Given/When/Then acceptance criteria, and
  measurable non-functional requirements. Trigger whenever a user says things
  like "write requirements for...", "draft user stories for...", "turn this into
  acceptance criteria", "spec out this feature", "we need requirements for
  document upload / notifications / approvals / access control / export /
  search / an API / an audit trail", or "make this requirement testable / less
  vague". Also the right skill for high-level requirements first, then refining
  them into detailed ones after a validation meeting. Comes with battle-tested
  patterns for common features so you don't rediscover the same detail each time.
model: opus
---

# Requirements Writer

The core move of good requirements work: take something vague and make it
**concrete, testable, and traceable**. "The system should let users upload
documents quickly and securely" hides a decision behind every word. This skill
turns that kind of ask into requirements a developer can build and a tester can
verify — without inventing business rules that nobody agreed to.

This is the *writing* step. If the request is still fuzzy, elicitation comes
first (see the **elicitation-planner** skill). When drafts exist and need
scrutiny, hand off to **requirements-reviewer**.

## What this skill produces

Pick what the user actually needs — you rarely need all of them at once:

- **Functional requirements** — "The system shall…" statements, one testable
  behaviour each.
- **User stories** — INVEST-compliant, `As a / I want / so that`, with acceptance
  criteria.
- **Acceptance criteria** — Given/When/Then, covering happy path, negative,
  boundary, permission, error, and data-validation scenarios.
- **Non-functional requirements** — performance, security, availability,
  usability, with *measurable* targets.
- **A full AI-ready requirement** — a single, traceable requirement with source
  and confidence recorded.

## Workflow

### Step 1 — Gather the inputs

Ask for what you need to write something real, and stop when you have enough:

- The feature, requirement, or need (paste it as-is).
- The business goal / why it matters.
- Known users or roles.
- Known constraints (tech, legal, data, deadlines).

If key inputs are missing, do not fill them with invention. Draft what the input
supports and collect the gaps under **Open Questions** in the output.

### Step 2 — Reach for a pattern first

Many requests are variations on a handful of recurring features. Before writing
from scratch, check `references/patterns/` — each file carries the hard-won
detail (fields, functional requirements, acceptance criteria, NFR considerations,
and an AI review prompt) for a common feature:

| If the ask is about… | Read |
|---|---|
| File / document uploads | `patterns/document-upload.md` |
| Emails, alerts, in-app messages | `patterns/notifications.md` |
| Review / sign-off / authorization flows | `patterns/approvals.md` |
| Roles, permissions, data scope (RBAC) | `patterns/access-control.md` |
| Search, filters, sorting, pagination | `patterns/search-and-filtering.md` |
| CSV / Excel / PDF exports | `patterns/data-export.md` |
| Inbound/outbound APIs, retries, idempotency | `patterns/integration-api.md` |
| Recording who did what and when | `patterns/audit-trail.md` |
| Treating an AI prompt as a requirement | `patterns/AI-Prompt-Is-The-New-Requirement.md` |

Use the pattern as a checklist of what a *complete* version of that feature
covers, then tailor every line to the user's domain, glossary, and constraints.
Never ship the generic wording verbatim — it is scaffolding, not the answer.

### Step 3 — Draft, using the right method

Read the method file that matches the deliverable and apply it as the facilitator
(don't paste the raw prompt at the user):

- User stories → `references/user-story-generator.md`
- Acceptance criteria → `references/acceptance-criteria-generator.md`
- Non-functional requirements → `references/nfr-generator.md`

Shape the final artifact with the matching template so it stays traceable:

- A complete requirement → `references/ai-ready-requirement.md`
- A single NFR → `references/nfr-specification.md`
- A decision worth recording (ADR) → `references/decision-record.md`

### Step 4 — Make it concrete

The value is in killing vagueness. For every subjective word — *fast, secure,
easy, appropriate, flexible* — either replace it with a measurable target or list
it as an open question. Prefer:

> ✅ "…upload **PDF** files up to **20 MB**, **virus-scanned before** they become
> available, **visible only to the customer and reviewers in the owning
> department**."

over "upload documents quickly and securely." A quick before/after and a full
worked example live in `references/examples/`.

### Step 5 — Self-check before handing over

Run the draft against the relevant checklist and fix what it catches:

- `references/checklists/requirement-quality.md` — completeness, clarity,
  testability, traceability.
- `references/checklists/user-story-quality.md` — INVEST plus AI checks.
- `references/checklists/nfr-checklist.md` — measurable non-functional targets.

Record **source**, **confidence**, and **open questions** on each requirement so
the next reader knows what is grounded and what still needs confirming — that is
what makes a requirement "AI-ready" and safe to act on.

## Principles

- **Testable or it doesn't count.** If QA can't write a test from it, it isn't
  done.
- **Don't invent business rules.** Surface gaps as Open Questions; let a human
  fill them.
- **Traceable by default.** Tie each requirement to a source and a business goal.
- **High-level first, then detail.** It's fine to draft a coarse version, validate
  it with the business, then refine — that loop is the job.
- **Ground every line.** Use only what the input provides — never invent business
  rules, roles, field names, numbers, or sources. Label inferences as **Assumption**
  and route unknowns back to a human under **Open Questions** rather than filling them.
- **Concise over complete-looking.** Produce only what was asked — no preamble, no
  restating the input. Include only the sections the input supports; omit what doesn't
  apply instead of padding it. One testable statement per line; stop when the request
  is met.
