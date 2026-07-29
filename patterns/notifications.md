# Notification Requirement Pattern

## Purpose

Use this pattern when a system needs to inform users about important events, status changes, required actions, exceptions, or deadlines.

Notifications are often simple at first, but they can quickly become complex because of channels, timing, preferences, failures, and regulatory constraints.

---

## Generic Requirement

The system shall notify the relevant user when a business event requires their attention.

---

## Example Requirement

The system shall notify the assigned reviewer when a submitted request is ready for review.

---

## Common Notification Events

- Request submitted
- Request approved
- Request rejected
- Task assigned
- Task overdue
- Document uploaded
- Document rejected
- Status changed
- Comment added
- Exception detected
- Deadline approaching

---

## Notification Channels

| Channel | Example Use |
|---|---|
| Email | Formal notifications and audit-relevant communication |
| In-app notification | Work queue and task updates |
| SMS | Time-critical alerts |
| Push notification | Mobile-first workflows |
| Teams / chat message | Collaboration-heavy environments |

---

## Requirement Fields

| Field | Description |
|---|---|
| Trigger Event | What causes the notification? |
| Recipient | Who receives the notification? |
| Channel | How is the notification sent? |
| Content | What information is included? |
| Timing | When is the notification sent? |
| Retry Rule | What happens if delivery fails? |
| Audit Requirement | Is the notification logged? |
| Opt-in / Opt-out | Can the user configure preferences? |

---

## Acceptance Criteria

### AC-01: Notification Sent

Given a request is submitted

When the request status changes to `Pending Review`

Then the assigned reviewer shall receive a notification.

---

### AC-02: Notification Content

Given a reviewer receives a notification

When the notification is opened

Then it shall contain:

- Request ID
- Request title
- Requester name
- Submission date
- Link to the request

---

### AC-03: Notification Audit

Given a notification is sent

When delivery is attempted

Then the system shall record:

- Recipient
- Channel
- Timestamp
- Delivery status

---

### AC-04: Failed Delivery

Given a notification cannot be delivered

When the delivery attempt fails

Then the system shall mark the notification as failed and make the failure visible for operational review.

---

## Non-Functional Considerations

- Notifications should not expose sensitive information unnecessarily.
- Notifications should be delivered within the agreed service level.
- Notification content should be understandable without requiring technical knowledge.
- Duplicate notifications should be avoided.
- Notification rules should be configurable where business needs vary.

---

## AI Review Prompt

```text
Act as a Senior Requirements Engineer.

Review the following notification requirement.

Check for:

1. Missing trigger event
2. Missing recipient
3. Missing channel
4. Missing timing expectation
5. Missing notification content
6. Missing failure handling
7. Missing audit requirement
8. Privacy or confidentiality risks
9. Ambiguous wording

Return findings as a markdown table with:

- Issue
- Risk
- Suggested improvement
- Severity
```
