# Search and Filtering Requirement Pattern

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

Use this pattern when users need to find records in a list, table, or dataset — free-text
search, structured filters, sorting, and pagination.

Search looks trivial until you ask what fields are searched, how matching works, what happens
with no results, and how permissions affect what a user is allowed to find.

---

## Generic Requirement

The system shall allow users to find relevant records using search terms and filters, and
shall only return records the user is permitted to see.

---

## Example Requirement

The system shall allow a reviewer to search requests by ID, title, and requester name, and to
filter by status and submission date.

---

## Core Requirement Fields

| Field | Description |
|---|---|
| Searchable Fields | Which fields does a text search match? |
| Match Rules | Exact, prefix, partial, fuzzy? Case sensitive? |
| Filters | Which structured filters are available? |
| Combining | Are filters combined with AND or OR? |
| Sorting | Which fields are sortable, and what is the default order? |
| Pagination | How many results per page? |
| Permissions | Are results limited to what the user may access? |
| Empty State | What is shown when there are no results? |
| Performance | Expected response time at expected data volume? |

---

## Example Functional Requirements

### FR-001: Text Search

The system shall return records whose configured searchable fields match the user's search
term.

---

### FR-002: Apply Filters

The system shall allow users to narrow results using the defined filters.

---

### FR-003: Respect Permissions

The system shall exclude records the user is not permitted to view from all search and filter
results.

---

### FR-004: Sort Results

The system shall allow users to sort results by the defined sortable fields.

---

### FR-005: Paginate Results

The system shall return results in pages of a configured size.

---

## Acceptance Criteria

### AC-01: Matching Search

Given records exist whose title contains "invoice"

When the user searches for "invoice"

Then the system shall return those records.

---

### AC-02: Combined Filters

Given the user filters by status `Pending` and date range this month

When the filters are applied

Then the system shall return only requests matching both conditions.

---

### AC-03: Permission-Scoped Results

Given a record the user is not permitted to view matches the search term

When the user searches

Then the system shall not return that record.

---

### AC-04: No Results

Given no records match the search term and filters

When the search runs

Then the system shall show a clear empty-state message and no error.

---

### AC-05: Sort Order

Given results are displayed

When the user sorts by submission date descending

Then the system shall order results from newest to oldest.

---

## Non-Functional Considerations

- Search should return results within the agreed response time at expected data volume.
- Partial input should give useful results without requiring exact matches, where appropriate.
- Search and filter state should be shareable or preserved when the user navigates back.
- Result counts should be accurate, including under permission scoping.
- The system should handle special characters and very long input safely.
- Search should degrade gracefully rather than error when the dataset is large.

---

## AI Review Prompt

```text
Act as a Senior Requirements Engineer.

Review the following search and filtering requirement.

Check for:

1. Which fields are searchable
2. Match rules (exact, prefix, partial, fuzzy, case sensitivity)
3. Available filters and how they combine (AND / OR)
4. Sorting options and default order
5. Pagination behavior
6. Permission scoping of results
7. Empty-state and error handling
8. Performance expectations at data volume
9. Handling of special characters and long input
10. Ambiguous wording

Return findings as a markdown table with:

- Issue
- Risk
- Suggested improvement
- Severity
```
