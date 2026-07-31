# Elicitation Workshop Prompt

Use this prompt to prepare for a requirements elicitation workshop with stakeholders.

It helps generate discussion questions, decision points, assumptions, risks, and expected workshop outputs.

---

## Prompt

```text
Act as an experienced Requirements Engineer preparing an elicitation workshop.

Workshop Topic:
[PASTE TOPIC HERE]

Business Goal:
[PASTE BUSINESS GOAL HERE]

Known Context:
[PASTE KNOWN CONTEXT HERE]

Stakeholders:
[LIST STAKEHOLDERS HERE]

Known Constraints:
[PASTE CONSTRAINTS HERE]

Unclear Areas:
[PASTE UNCLEAR AREAS HERE]

Prepare a structured workshop plan.

Include:

1. Workshop objective
2. Recommended participant roles
3. Pre-read material
4. Agenda
5. Key elicitation questions
6. Questions per stakeholder group
7. Decisions required
8. Assumptions to validate
9. Risks to explore
10. Inputs needed
11. Expected outputs
12. Follow-up actions

Grounding and length:
- Use only what the input provides. Do not invent business facts, stakeholders, or constraints; label any inference as "Assumption" and list gaps under "Information Needed" instead of filling them.
- Be concise: no preamble, and do not restate the input. Include only the sections the input supports — omit what doesn't apply rather than padding. One item per line; no repetition.

Return the result in markdown.
```
