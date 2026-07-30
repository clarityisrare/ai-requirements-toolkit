# Access Control Requirement Pattern

## Purpose

Use this pattern when different users must be allowed to see and do different things —
role-based access control (RBAC), permissions, and authorization rules.

Access control is easy to state ("only managers can approve") and hard to get right: it
touches roles, permissions, ownership, data scoping, delegation, and the difference between
"can't see the button" and "can't perform the action".

---

## Generic Requirement

The system shall restrict each action and each data view to users who hold the required
permission for that action or data.

---

## Example Requirement

The system shall allow only users with the `Reviewer` role to approve requests, and shall
restrict reviewers to requests within their own department.

---

## Key Concepts

| Concept | Meaning |
|---|---|
| Authentication | Proving who the user is |
| Authorization | Deciding what the user may do |
| Role | A named bundle of permissions (e.g. Reviewer, Admin) |
| Permission | A single allowed action (e.g. `approve_request`) |
| Data scope | Which records a role may act on (own / team / all) |
| Ownership | Rights a user has over records they created |

---

## Core Requirement Fields

| Field | Description |
|---|---|
| Roles | What roles exist? |
| Permissions | What actions does each role allow? |
| Data Scope | Which records can each role access (own, team, org, all)? |
| Default Access | What can an authenticated user do by default? |
| Least Privilege | Is access denied unless explicitly granted? |
| Delegation | Can permissions be temporarily granted or delegated? |
| Admin Rights | Who manages roles and assignments? |
| Enforcement Point | Is the rule enforced server-side, not only in the UI? |
| Audit | Are access grants, changes, and denials logged? |

---

## Example Functional Requirements

### FR-001: Enforce Authorization Server-Side

The system shall enforce every access rule on the server, regardless of what the client
displays.

---

### FR-002: Deny by Default

The system shall deny any action for which the user has no explicit permission.

---

### FR-003: Scope Data to Role

The system shall return only the records a user's role and data scope permit.

---

### FR-004: Manage Roles

The system shall allow an administrator to create roles, assign permissions, and assign
users to roles.

---

### FR-005: Log Access Changes

The system shall record all role assignments, permission changes, and denied-access
attempts.

---

## Acceptance Criteria

### AC-01: Permitted Action

Given a user holds the `Reviewer` role

When they open a request in their department

Then the system shall allow them to approve it.

---

### AC-02: Denied Action

Given a user does not hold the `Reviewer` role

When they attempt to approve a request

Then the system shall deny the action and record the attempt.

---

### AC-03: Data Scope

Given a reviewer belongs to Department A

When they list requests

Then the system shall show only requests from Department A.

---

### AC-04: Server-Side Enforcement

Given the approve control is hidden in the UI

When a user calls the approve API directly without permission

Then the system shall reject the call.

---

### AC-05: Least Privilege

Given a newly created role with no permissions

When a user with that role signs in

Then the system shall allow no restricted actions.

---

## Non-Functional Considerations

- Authorization checks should not add noticeable latency to common actions.
- Access rules should be configurable without code changes where policy varies.
- The UI should hide or disable actions the user cannot perform, in addition to server-side enforcement.
- Denied-access attempts should be observable for security monitoring.
- Role and permission models should stay understandable as they grow.
- Removing a user's role should take effect promptly, including on active sessions where required.

---

## AI Review Prompt

```text
Act as a Senior Requirements Engineer with a security mindset.

Review the following access control requirement.

Check for:

1. Clear list of roles
2. Clear permissions per role
3. Data scope (own / team / org / all)
4. Deny-by-default / least privilege
5. Server-side enforcement, not UI-only
6. Delegation and temporary access
7. Who administers roles and permissions
8. Logging of grants, changes, and denials
9. Handling of role removal and active sessions
10. Separation of authentication vs authorization
11. Ambiguous wording

Return findings as a markdown table with:

- Issue
- Risk
- Suggested improvement
- Severity
```
