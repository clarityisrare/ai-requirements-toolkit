# Example: AI Review — Sample Output

This shows what the review prompts in this toolkit actually return, so you know what to expect
and how to read it. The prompt used is [`requirement-review.md`](../requirement-review.md).

---

## Input requirement

> REQ-030 — The system shall let managers approve time-off requests. Approved requests should
> update the calendar. The system should be fast and handle lots of users.

---

## Sample AI output

| # | Finding | Type | Risk | Suggested improvement | Severity |
|---|---|---|---|---|---|
| 1 | "managers" is undefined — line manager, department manager, or any manager? | Ambiguity | Wrong person approves, or nobody can | Define the approver rule (e.g. the requester's direct line manager) | HIGH |
| 2 | No rejection path — only approval is described | Missing business rule | Requests cannot be declined or returned | Add reject and request-changes outcomes with comments | HIGH |
| 3 | "update the calendar" — which calendar, and what if the update fails? | Ambiguity + missing error handling | Approved leave not reflected; double-booking | Name the target calendar and define failure handling | MEDIUM |
| 4 | "fast" is not measurable | Testability | Cannot be verified or agreed | Set a target, e.g. approval action completes under 2 s at the 95th percentile | MEDIUM |
| 5 | "lots of users" is not a number | Testability | Capacity cannot be designed or tested | State expected and peak concurrent users | MEDIUM |
| 6 | No mention of who may see or audit approvals | Traceability / security | Decisions not accountable | Add audit of approval decisions (see Audit Trail pattern) | LOW |
| 7 | Segregation of duties not addressed | Missing business rule | A manager could approve their own request | Prevent self-approval | LOW |

---

## How to use this output

1. **Do not accept it blindly.** Run it through the
   [AI Output Validation checklist](../../assets/ai-output-validation.md) first.
2. **Confirm, don't assume.** Findings 1 and 2 change behavior — take them to the stakeholder,
   don't guess the answer.
3. **Turn HIGH findings into changes.** Each HIGH finding should become an edit to the
   requirement or a tracked open question before the item is called ready.
4. **Reuse the patterns.** Findings 6 and 7 point straight at the Audit Trail and
   Approval Workflow patterns in the requirements-writer skill — apply them rather
   than reinventing the wording.

---

## The rewritten requirement (after acting on the findings)

> **REQ-030 — Time-off approval**
> The system shall route each submitted time-off request to the requester's **direct line
> manager**, who may **approve, reject (with a comment), or request changes**. A manager shall
> **not be able to approve their own request**. On approval, the system shall add the leave to
> the **company calendar**; if the calendar update fails, the request stays approved and the
> failure is flagged for operational review. The approval action shall complete in **under 2
> seconds at the 95th percentile**, supporting **up to 500 concurrent users**. All approval
> decisions shall be **recorded in the audit trail**.

Seven vague or missing points, resolved — that is a normal, and very fast, review cycle with
AI doing the first pass and a human making the calls.
