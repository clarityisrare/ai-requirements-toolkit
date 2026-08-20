# Workshop Plan (template)

Produce this in your reply, tailored to the request. Fill each section from the
raw request and the Open Questions list from Step 2. Mark anything you do not know
as Open rather than inventing it, and keep the plan to what the input supports.

## Structure

**Objective** — one sentence: what this meeting must decide or uncover.

**Participants** — who to invite, by role, and why each is needed.

**Pre-read** — what to send ahead (the requirements contract, the draft under
validation, the systems involved).

**Agenda** — timed:

| Time | Item | Purpose |
|------|------|---------|
| 0:00 | ... | ... |

**Key questions, grouped by stakeholder** — each question tied to an item on the
Open Questions list, so the meeting closes a real gap. For a validation meeting, reshape these into
confirmation ("Did I capture this correctly? Where am I wrong?") and drill the
specific gaps rather than opening fresh discovery.

- *Sponsor:* ...
- *Operations:* ...

**Decisions required** — what must be agreed by the end.

**Assumptions to validate** — the guesses this meeting confirms or kills.

**Risks to explore** — what could derail delivery, to surface early.

**Expected outputs** — the artifacts the meeting should produce.

**Follow-up actions** — who does what next, and by when.

---

## Worked example

**Request in:** "The business wants customers to be able to upload documents to
their account. That's all we were told."

**Abbreviated plan out:**

**Objective** — Agree what "document upload" must do for customers and the
business, and surface the constraints (file types, size, security) before drafting.

**Participants** — Product owner (owns scope), a customer-facing rep (real use),
security/compliance (upload risk), an engineer (feasibility).

**Agenda**

| Time | Item | Purpose |
|------|------|---------|
| 0:00 | Frame the request | Shared understanding of the problem |
| 0:10 | Who uploads what, and why | Ground the use in real scenarios |
| 0:30 | Constraints: file types, size, retention, security | Close the biggest unknowns |
| 0:50 | Risks and decisions | Assign owners |

**Key questions, grouped by stakeholder**

- *Product owner:* Which documents, and what happens after upload — self-service or reviewed?
- *Security/compliance:* What rules govern storing and scanning customer files? What retention period?
- *Customer rep:* When do customers try to do this today, and how do they work around its absence?

**Decisions required** — Allowed file types and size limit; whether uploads are
reviewed before use.

**Open** — Volume expectations, retention policy, and integration with existing
storage are unknown; carry them into the session as open questions rather than
guessing.
