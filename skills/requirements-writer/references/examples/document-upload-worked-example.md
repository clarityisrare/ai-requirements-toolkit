# Example: Document Upload, Start to Finish

This walks a single, realistic ask through the toolkit — from a one-line request to
review-ready requirements — using the [Document Upload pattern](../patterns/document-upload.md).

---

## Step 0 — The raw ask

A stakeholder says, in a meeting:

> "Customers need to be able to send us their proof of address."

That is a need, not a requirement. Here is how the toolkit turns it into something a team can
build and test.

---

## Step 1 — Fill in the pattern's Core Fields

Using the field table from the pattern as a checklist of questions to ask:

| Field | Answer (from stakeholder) |
|---|---|
| File Type | PDF, JPG, PNG |
| File Size | Up to 10 MB |
| User Role | Authenticated customer |
| Business Object | Customer application |
| Metadata | File name, type, size, upload time, uploader, application ID |
| Validation | Type + size + virus scan |
| Storage | Encrypted document store, retained 7 years |
| Access Control | Customer (own) + reviewers in owning department |
| Audit Trail | Upload, replace, download, delete |
| Retention | 7 years after application closure |

Two answers were not known in the room — **retention** and **who may delete** — so they go to
Open Questions rather than being invented.

---

## Step 2 — Write the requirement and criteria

**REQ-021 — Customer uploads proof of address**

> The system shall allow an authenticated customer to upload a PDF, JPG, or PNG file up to
> 10 MB as proof of address on their application. Files shall be virus-scanned before becoming
> available, stored encrypted, and visible only to the customer and reviewers in the owning
> department.

Acceptance criteria (abbreviated — see the pattern for the full set):

- **AC-01** Given a valid file under 10 MB, when uploaded, then it is attached to the application.
- **AC-02** Given a disallowed file type, when uploaded, then it is rejected with a clear message.
- **AC-03** Given a file over 10 MB, when uploaded, then it is rejected and the limit is shown.
- **AC-04** Given a file fails the virus scan, when the result returns, then access is blocked and the failure recorded.

---

## Step 3 — Capture what you did not know

```text
Open Questions
- Retention period after application closure? (assumed 7 years — needs Compliance)
- Who may delete an uploaded document, and can a customer replace one?
- Is there a maximum number of files per application?
```

---

## Step 4 — Run the pattern's AI Review prompt

Paste REQ-021 into the pattern's [AI Review Prompt](../patterns/document-upload.md#ai-review-prompt).
A representative result:

| Issue | Risk | Suggested improvement | Severity |
|---|---|---|---|
| No maximum file count | Customers upload dozens of files, storage and review load grow | Define a per-application limit | Medium |
| Retention assumed, not confirmed | Compliance breach if wrong | Confirm retention with Compliance before build | High |
| Delete/replace rights unspecified | Evidence could be altered after review | Define who may replace/delete and whether it is audited | High |
| "Proof of address" not defined | Reviewers apply different standards | Add accepted document types to the glossary | Low |

---

## Step 5 — Validate the AI output

Before accepting any of the above, run it through the
[AI Output Validation checklist](../checklists/ai-output-validation.md). The retention finding
is **Inferred** (the AI flagged an assumption *we* made) — valid. Nothing was invented, so it
passes source-grounding.

---

## The result

One vague sentence became a testable requirement, four acceptance criteria, three tracked open
questions, and a prioritized review — in minutes, with a human owning every decision. That is
the whole point of the toolkit: **AI accelerates the work; the Requirements Engineer stays
accountable for it.**
