# Acceptance Criteria Generator Prompt

Use this prompt to turn a requirement, feature idea, user story, or business rule into structured acceptance criteria.

The output should always be reviewed by a Requirements Engineer, Product Owner, QA specialist, or relevant subject matter expert before use.

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

Return the result as a markdown table.

Do not invent business rules.
If information is missing, list it under "Open Questions".
Clearly label any assumption as "Assumption".
```
