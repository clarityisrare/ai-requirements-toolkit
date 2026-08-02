# Non-Functional Requirements (NFR) Generator Prompt

Use this prompt to surface the non-functional requirements a feature needs — performance,
security, availability, usability, and more. Functional requirements say *what* the system
does; NFRs say *how well* it must do it.

Review the output with architects and relevant SMEs, and turn vague targets into measurable
ones. See the companion [NFR checklist](../checklists/nfr-checklist.md).

---

## Prompt

```text
Act as a Senior Requirements Engineer and Solution Architect.

For the feature described below, generate the relevant non-functional requirements.

Feature:
[PASTE FEATURE HERE]

Context (users, volume, criticality, environment):
[PASTE CONTEXT HERE]

Known Constraints:
[PASTE CONSTRAINTS HERE]

Cover these NFR categories where relevant:

1. Performance and response time
2. Scalability and expected load
3. Availability and reliability
4. Security
5. Privacy and data protection
6. Usability and accessibility
7. Maintainability
8. Compatibility and interoperability
9. Observability (logging, monitoring, alerting)
10. Compliance and legal
11. Localization / internationalization

For each NFR, provide:

- ID
- Category
- Requirement statement
- Measurable target (a number or condition, not "fast" or "secure")
- How it can be verified
- Assumption, if the target was inferred

Rules:
- Make every target measurable. If you cannot, mark it "Needs a target" and explain what
  information is required.
- Do not invent business or compliance constraints; list unknowns under "Open Questions".

Return the result as a markdown table, grouped by category.
```
