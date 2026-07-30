# Audit Trail Requirement Pattern

## Purpose

Use this pattern when a system must keep a reliable, tamper-evident record of who did what
and when — typically for accountability, troubleshooting, dispute resolution, or regulatory
compliance.

Audit trail requirements look simple ("log the changes") but quickly raise questions about
which events to capture, how much detail to store, who may read the log, and how long it is
retained.

---

## Generic Requirement

The system shall record an immutable audit event for every action that creates, changes, or
removes business-relevant data.

---

## Example Requirement

The system shall record the previous value and the new value whenever a user updates a
customer record, together with the user identity and a timestamp.

---

## Core Requirement Fields

| Field | Description |
|---|---|
| Audited Events | Which actions are recorded (create, update, delete, read, export, login)? |
| Actor | Who performed the action (user ID, service account, system)? |
| Timestamp | When did it happen, and in which time zone / format? |
| Action Type | What kind of action was performed? |
| Target | Which record or object was affected? |
| Old / New Value | What changed (before and after)? |
| Source | Where did the action originate (UI, API, batch job, integration)? |
| Immutability | How is the log protected from edits or deletion? |
| Access Control | Who may read, export, or purge the audit trail? |
| Retention | How long are audit events kept, and how are they disposed of? |

---

## Example Functional Requirements

### FR-001: Record Data Changes

The system shall record an audit event for every create, update, and delete action on
business-relevant data.

---

### FR-002: Capture Actor and Time

The system shall record the acting user identity and a timestamp for each audit event.

---

### FR-003: Capture Before and After Values

The system shall record the previous value and the new value for each changed field.

---

### FR-004: Protect Audit Integrity

The system shall prevent audit events from being modified or deleted by application users.

---

### FR-005: Control Audit Access

The system shall restrict read and export of the audit trail to authorized roles.

---

### FR-006: Apply Retention Rules

The system shall retain audit events for the configured retention period and dispose of
them according to policy.

---

## Acceptance Criteria

### AC-01: Change Recorded

Given a user updates a customer record

When the change is saved

Then the system shall store the original value and the new value in the audit trail.

---

### AC-02: Actor and Timestamp

Given any audited action is performed

When the audit event is created

Then the system shall record the acting user identity and a timestamp.

---

### AC-03: Immutable Log

Given an audit event exists

When any user attempts to modify or delete it

Then the system shall prevent the change and record the attempt.

---

### AC-04: Restricted Access

Given a user without the audit-viewer role

When they attempt to open the audit trail

Then the system shall deny access.

---

### AC-05: Retention

Given an audit event has passed its retention period

When the retention job runs

Then the system shall dispose of the event according to policy.

---

## Non-Functional Considerations

- Writing an audit event should not noticeably slow down the user action it records.
- The audit trail should be stored durably and survive application restarts or failures.
- Audit records should not expose more sensitive data than the event requires.
- The log should remain readable and queryable as its volume grows.
- Time should be recorded consistently (e.g. UTC) to keep events comparable across systems.
- Failure to write an audit event should be detected and handled, not silently ignored.

---

## AI Review Prompt

```text
Act as a Senior Requirements Engineer.

Review the following audit trail requirement.

Check for:

1. Which events are audited (create, update, delete, read, export, login)
2. Actor identification
3. Timestamp and time zone handling
4. Before and after values
5. Source of the action
6. Immutability and tamper protection
7. Access control for reading and exporting the log
8. Retention and disposal rules
9. Performance impact
10. Privacy of sensitive data in the log
11. Handling of failed audit writes
12. Ambiguous wording

Return findings as a markdown table with:

- Issue
- Risk
- Suggested improvement
- Severity
```
