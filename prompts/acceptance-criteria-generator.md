# Acceptance Criteria Generator Prompt

Use this prompt to turn a requirement, feature idea, user story, or business rule into structured acceptance criteria.

The output should always be reviewed by a Requirements Engineer, Product Owner, QA specialist, or relevant subject matter expert before use. See the companion [review checklist](./acceptance-criteria-review-checklist.md).

---

## Prompt

```text
Act as a Senior Requirements Engineer and QA-minded Business Analyst.

Your task is to generate clear, testable acceptance criteria for the requirement below.

Requirement:
[PASTE REQUIREMENT HERE]

Business Context:
[PASTE BUSINESS CONTEXT HERE]

Known Constraints:
[PASTE CONSTRAINTS HERE]

Stakeholders:
[PASTE STAKEHOLDERS HERE]

Generate acceptance criteria using Given / When / Then format.

Include:

1. Happy path scenarios
2. Negative scenarios
3. Boundary conditions
4. Permission or role-based scenarios
5. Error handling scenarios
6. Data validation scenarios
7. Audit or traceability scenarios, if relevant
8. Non-functional acceptance criteria, if relevant

For each acceptance criterion, provide:

- ID
- Scenario name
- Given / When / Then
- Requirement or rule covered
- Open questions, if any

Grounding and length:
- Use only what the input provides. Do not invent business rules, roles, names, numbers, or sources; label any inference as "Assumption" and list gaps under "Open Questions" instead of filling them.
- Be concise: no preamble, and do not restate the input. Cover only the scenario types the requirement supports — omit those that don't apply rather than padding. One criterion per row; no repetition.

Return the result as a markdown table.
```
