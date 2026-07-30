# Approval Workflow Requirement Pattern

## Purpose

Use this pattern when a request, document, or change must be reviewed and authorized before
it can proceed. Approvals appear in expense sign-off, content publishing, onboarding, change
management, and many other workflows.

Approval requirements become complex around multi-level chains, delegation, timeouts,
segregation of duties, and what happens when a request is rejected or changed.

See the companion diagram: [`diagrams/approval-process.mmd`](../diagrams/approval-process.mmd).

---

## Generic Requirement

The system shall route a submitted request to the appropriate approver(s) and record the
outcome before the request can proceed.

---

## Example Requirement

The system shall require a line manager to approve any expense request over 500 EUR before
it is sent for payment.

---

## Approval States

- Draft
- Pending Review
- Approved
- Rejected
- Changes Requested (optional)
- Withdrawn (optional)

---

## Core Requirement Fields

| Field | Description |
|---|---|
| Trigger | What submits an item for approval? |
| Approver(s) | Who must approve, and in what order? |
| Levels | Is approval single-step or multi-level? |
| Rules | What conditions decide the approver or path (amount, type, risk)? |
| Delegation | Can an approver delegate or be substituted when absent? |
| Segregation of Duties | Can the requester also approve? |
| Timeout / Escalation | What happens if no decision is made in time? |
| Comments | Are comments required, especially on rejection? |
| Outcome Record | How is the decision and its author stored? |
| Notifications | Who is informed at submission and decision? |

---

## Example Functional Requirements

### FR-001: Submit for Approval

The system shall allow an authorized requester to submit an item for approval.

---

### FR-002: Route to Approver

The system shall route the request to the correct approver based on the configured rules.

---

### FR-003: Record Decision

The system shall record each approval decision with the approver identity, timestamp, and
any comments.

---

### FR-004: Require Rejection Reason

The system shall require a comment when a request is rejected.

---

### FR-005: Enforce Segregation of Duties

The system shall prevent a user from approving a request they submitted.

---

### FR-006: Escalate on Timeout

The system shall escalate a request that is not actioned within the configured time.

---

## Acceptance Criteria

### AC-01: Approve

Given a request is submitted

When the approver accepts it

Then the status shall become Approved.

---

### AC-02: Reject with Comment

Given a request is pending review

When the approver rejects it and provides a comment

Then the status shall become Rejected and the comment shall be recorded.

---

### AC-03: Rejection Requires a Reason

Given an approver rejects a request without a comment

When they attempt to submit the decision

Then the system shall block the action and ask for a reason.

---

### AC-04: Segregation of Duties

Given a user is the requester of an item

When they open that item for approval

Then the system shall not allow them to approve it.

---

### AC-05: Escalation

Given a request has been pending longer than the configured limit

When the escalation job runs

Then the system shall escalate or reassign the request and notify the relevant party.

---

## Non-Functional Considerations

- Approval routing should be configurable without code changes where business rules vary.
- The current status and pending approver should be visible to authorized users at any time.
- Decisions and their authors should be stored durably for later audit.
- Notifications should reach approvers promptly so requests are not silently delayed.
- Delegation and absence handling should avoid blocking the workflow.
- Concurrent decisions on the same request should be handled predictably.

---

## AI Review Prompt

```text
Act as a Senior Requirements Engineer.

Review the following approval workflow requirement.

Check for:

1. Trigger for submission
2. Approver identification and order
3. Single vs multi-level approval
4. Rules that determine the approval path
5. Delegation and absence handling
6. Segregation of duties
7. Timeout and escalation behavior
8. Required comments, especially on rejection
9. Recording of the decision and its author
10. Notifications to relevant parties
11. Handling of withdrawal or resubmission
12. Ambiguous wording

Return findings as a markdown table with:

- Issue
- Risk
- Suggested improvement
- Severity
```
