# Data Export Requirement Pattern

## Contents

- Purpose
- Generic Requirement
- Example Requirement
- Core Requirement Fields
- Example Functional Requirements
- Acceptance Criteria
- Non-Functional Considerations
- AI Review Prompt

## Purpose

Use this pattern when users need to take data out of the system — CSV/Excel downloads, PDF
reports, or scheduled data extracts.

Exports raise real questions about which columns leave the system, who is allowed to export,
how large exports are handled, and how the act of exporting is recorded.

---

## Generic Requirement

The system shall allow authorized users to export the data they are permitted to view, in a
defined format, and shall record each export.

---

## Example Requirement

The system shall allow a reviewer to export the currently filtered list of requests to CSV,
including only the columns they are permitted to see.

---

## Core Requirement Fields

| Field | Description |
|---|---|
| Format | CSV, Excel, PDF, JSON? |
| Scope | All data, current filter, or selected rows? |
| Columns | Which fields are included? Are sensitive fields excluded? |
| Permissions | Who may export, and does export respect data scope? |
| Volume | What is the maximum export size, and how are large exports handled? |
| Delivery | Direct download, email link, or scheduled drop? |
| Encoding | Character encoding and delimiter (e.g. UTF-8, comma)? |
| Audit | Is each export logged with user, time, and scope? |
| Privacy | Are personal or regulated fields masked or excluded? |

---

## Example Functional Requirements

### FR-001: Export Permitted Data

The system shall export only the records and columns the requesting user is permitted to see.

---

### FR-002: Respect Current Filter

The system shall export the data matching the user's current filter and search, unless a full
export is explicitly chosen.

---

### FR-003: Handle Large Exports

The system shall handle exports above the inline threshold asynchronously and notify the user
when the file is ready.

---

### FR-004: Record the Export

The system shall record an audit event for each export, including user, timestamp, scope, and
row count.

---

### FR-005: Protect Sensitive Fields

The system shall exclude or mask sensitive fields in exports unless the user is explicitly
authorized to export them.

---

## Acceptance Criteria

### AC-01: Filtered Export

Given a reviewer has filtered requests to status `Pending`

When they export to CSV

Then the file shall contain only the pending requests they are permitted to see.

---

### AC-02: Permission-Scoped Columns

Given a user is not permitted to view a sensitive column

When they export the data

Then that column shall be excluded from the file.

---

### AC-03: Large Export

Given an export exceeds the inline size threshold

When the user requests it

Then the system shall process it asynchronously and notify the user when ready.

---

### AC-04: Export Audit

Given a user exports data

When the export completes

Then the system shall record the user, timestamp, scope, and row count.

---

### AC-05: Correct Format

Given a user exports to CSV

When the file is opened

Then it shall use the defined encoding and delimiter and open without corruption.

---

## Non-Functional Considerations

- Exports should complete within an acceptable time for expected data volumes.
- Very large exports should not degrade performance for other users.
- Exported files should use a stable, documented column order and format.
- Personal and regulated data should be handled per privacy and compliance rules.
- Download links, if used, should expire and be access-controlled.
- Failed exports should not leave partial or misleading files.

---

## AI Review Prompt

```text
Act as a Senior Requirements Engineer.

Review the following data export requirement.

Check for:

1. Export format(s)
2. Export scope (all / filtered / selected)
3. Included columns and excluded sensitive fields
4. Permission scoping (rows and columns)
5. Maximum size and handling of large exports
6. Delivery method (download, link, scheduled)
7. Encoding and delimiter
8. Audit logging of exports
9. Privacy and compliance handling
10. Failure handling
11. Ambiguous wording

Return findings as a markdown table with:

- Issue
- Risk
- Suggested improvement
- Severity
```
