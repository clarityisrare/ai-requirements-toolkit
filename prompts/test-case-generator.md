# Test Case Generator Prompt

Use this prompt to turn a requirement and its acceptance criteria into concrete, executable
test cases that QA can run.

The output should be reviewed by QA and mapped to your traceability matrix so every
requirement is covered by at least one test.

---

## Prompt

```text
Act as a Senior QA Engineer.

Generate test cases for the requirement and acceptance criteria below.

Requirement:
[PASTE REQUIREMENT HERE]

Acceptance Criteria:
[PASTE ACCEPTANCE CRITERIA HERE]

Known Constraints and Data:
[PASTE CONSTRAINTS / TEST DATA HERE]

Produce test cases that cover:

1. Happy path
2. Negative cases
3. Boundary values
4. Permission / role-based cases
5. Error handling and validation
6. Data edge cases (empty, maximum, special characters)

For each test case, provide:

- Test ID
- Linked requirement or acceptance criterion
- Title
- Preconditions
- Steps
- Test data
- Expected result
- Type (positive / negative / boundary)

Rules:
- Each acceptance criterion must be covered by at least one test case.
- Keep steps concrete enough for someone unfamiliar with the feature to execute.
- Note any acceptance criterion that cannot be tested as written, and why.

Return the result as a markdown table.
```
