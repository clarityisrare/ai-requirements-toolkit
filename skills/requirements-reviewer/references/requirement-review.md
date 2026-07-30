# Requirement Review Prompt

Use this prompt for a structured, risk-classified review of a single requirement.

---

## Prompt

```text
Act as a Senior Requirements Engineer.

Review the requirement below.

Identify:

1. Ambiguous terminology
2. Missing assumptions
3. Missing constraints
4. Missing business rules
5. Missing stakeholder perspectives
6. Testability issues
7. Security concerns
8. Traceability concerns

Classify findings:

HIGH
MEDIUM
LOW

For each finding provide:

- Description
- Risk
- Suggested improvement

Return the result as a markdown table.
```
