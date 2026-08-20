# Example: Vague vs Clear Requirement

Most requirements problems are not missing requirements — they are *vague* ones that everyone
reads differently. Here is the same requirement, before and after, with the reasoning that
takes you from one to the other.

---

## ❌ Before (vague)

> The system should let users upload documents quickly and securely, and notify the right
> people when something happens.

Why this hurts:

| Problem | Why it is a problem |
|---|---|
| "users" | Which users? All of them? Any role? |
| "documents" | Which file types? Any size? |
| "quickly" | Not measurable — 1 second? 30 seconds? |
| "securely" | Undefined — scanning? encryption? access control? |
| "the right people" | Who, exactly, and based on what rule? |
| "when something happens" | Which events trigger a notification? |

Every bold word above is an ambiguity finding — a term whose meaning is left for a
reader to guess.

---

## ✅ After (clear and testable)

**REQ-014 — Customer document upload**

> The system shall allow authenticated **customers** to upload **PDF** files up to **20 MB**
> as supporting evidence for an application. Each file shall be **virus-scanned before it
> becomes available**, and shall be **visible only to the customer and reviewers in the
> owning department**. When a customer completes an upload, the system shall **notify the
> assigned reviewer within 1 minute**.

Acceptance criteria:

- **AC-01 — Successful upload**
  Given an authenticated customer selects a PDF under 20 MB,
  When they upload it,
  Then the system attaches it to their application and confirms success.

- **AC-02 — Rejected file type**
  Given a customer selects a non-PDF file,
  When they attempt to upload,
  Then the system rejects it and shows the allowed format.

- **AC-03 — Security scan**
  Given an uploaded file fails the virus scan,
  When the result is received,
  Then the system blocks access and records the failure.

- **AC-04 — Reviewer notification**
  Given a customer completes an upload,
  When the upload succeeds,
  Then the assigned reviewer receives a notification within 1 minute.

---

## What changed

| Vague term | Made concrete as |
|---|---|
| users | authenticated customers |
| documents | PDF, up to 20 MB |
| quickly | (removed; replaced with a measurable notification SLA) |
| securely | virus scan before availability + role-scoped visibility |
| the right people | the assigned reviewer in the owning department |
| when something happens | on successful upload |

The clear version is longer — and that is the point. Every added word removes a decision that
would otherwise be made, differently, by developers, testers, and stakeholders after the fact.

---

## The moves you can reuse

1. **Name the actor.** Replace "users" with a specific role.
2. **Quantify every adjective.** "Fast" becomes a number; "large" becomes a limit.
3. **Unpack loaded words.** "Secure" is not a requirement — the scan, the encryption, and the
   access rule are.
4. **Attach a rule to every "right".** "The right people" must resolve to a rule anyone can apply.
5. **List the triggering events.** "When something happens" becomes named events.
6. **Add acceptance criteria.** If you cannot write a Given/When/Then, the requirement is not
   yet testable.
