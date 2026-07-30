---
name: elicitation-planner
description: >-
  Use at the very START of requirements work, before any requirement is written.
  Turn a thin, vague business request into a first-cut requirements contract, a
  stakeholder map, a domain glossary, and a facilitator-ready workshop plan.
  Trigger whenever a user says things like "business asked us for X", "we got a
  request to build...", "I need to run a requirements / discovery / kickoff
  workshop", "help me prepare for a stakeholder meeting", "what should I ask the
  business about...", or "I need to validate my understanding with stakeholders".
  Supports both the first DISCOVERY meeting and a later VALIDATION meeting that
  confirms drafted requirements. Once you understand the request, hand off to the
  requirements-writer skill to draft the requirements.
model: opus
---

# Elicitation Planner

Requirements work starts before a single requirement is written. A business
request usually arrives thin — "we need document upload", "customers should get
notified" — and every word hides a decision. This skill helps a Requirements
Engineer, Business Analyst, or Product Owner **prepare to talk to the business**:
frame the request, map who to involve, surface what is still unknown, and walk
into the room with a plan instead of a blank page.

The output of this skill is preparation, not the final requirements. When the
picture is clear enough to draft, hand off to the **requirements-writer** skill.

## The two moments this supports

Elicitation is not one meeting — it brackets the writing:

1. **Discovery** — the first conversation. The request is fresh and vague; the
   goal is to understand the domain, the real problem, and the constraints.
2. **Validation** — a later conversation, *after* high-level requirements exist.
   The goal is to replay "here is what I heard", confirm it, and close specific
   gaps with sharper questions.

Always establish which one you are preparing for first — the plan differs a lot.
Discovery is open and exploratory; validation is targeted and confirmatory.

## Workflow

### Step 1 — Capture the raw request

Ask the user for whatever they have, however thin:

- The request as it was received (paste, forward, or paraphrase).
- Who asked for it and why now (the business driver / trigger).
- Anything already known: constraints, deadlines, systems involved, prior
  decisions.
- Which moment this is: **discovery** or **validation**. If validation, also ask
  for the drafted requirements or understanding to be confirmed.

Do not invent business facts. If something is unknown, that is not a blocker —
unknowns are the raw material for the workshop agenda.

### Step 2 — Produce a first-cut requirements contract

Before planning any meeting, distil the request into a one-page contract so
everyone agrees on *what problem we are solving* before debating solutions. Use
the structure in `references/requirements-contract.md`. Fill what you can from the
request and explicitly mark the rest as **Open** — an honest "unknown" is more
useful than a confident guess.

Then extract an **Open Questions / Unknowns list** — every field you could not
fill, every ambiguous term, every unstated assumption. This list becomes the
backbone of the workshop agenda.

### Step 3 — Map the stakeholders

Identify who needs to be in the room and who is affected but absent. Use
`references/stakeholder-analysis.md` to classify by interest, influence, and how
to engage each group. Flag any perspective that is missing — the most expensive
requirements gaps come from a stakeholder nobody thought to ask.

### Step 4 — Plan the workshop

Read `references/elicitation-workshop.md` for the full structure to generate. Do
**not** paste that prompt at the user — you are the facilitator now. Produce a
concrete plan tailored to their request, including:

- Objective, recommended participants, and pre-read.
- A timed agenda.
- **Key elicitation questions**, grouped by stakeholder — and driven by the
  Open Questions list from Step 2, so the meeting closes real gaps.
- Decisions required, assumptions to validate, risks to explore.
- Expected outputs and follow-up actions.

For a **validation** meeting, reshape the questions around confirming the drafted
understanding ("Did I capture this correctly? Where am I wrong?") and drilling
into the specific gaps, rather than open discovery.

### Step 5 — Seed the glossary and risks (as they emerge)

Ambiguity is cheapest to kill early. As domain terms surface, start a shared
glossary using `references/glossary.md` (the `glossary-builder` prompt approach in
`references/glossary-builder.md` shows how to extract terms from notes or
transcripts if the user has raw material). Capture any risks that appear in
`references/risk-register.md`.

### Step 6 — Hand off

When the request is understood well enough to draft, say so plainly and point to
the **requirements-writer** skill to turn the discovery into high-level, then
detailed, requirements. Remind the user that a human — RE, PO, or SME — owns the
final call.

## Principles

- **Confirm, don't assume.** Everything the business said is a starting point,
  not a fact. Label assumptions as assumptions.
- **Unknowns are the agenda.** A good elicitation plan is organised around what
  you *don't* yet know.
- **One vocabulary.** Start the glossary early; a shared term prevents a dozen
  downstream misunderstandings.
- **Keep a human accountable** for every decision the workshop produces.
