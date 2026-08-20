# AI Output Validation Checklist

Use this checklist before accepting AI-generated requirements, user stories, acceptance criteria, summaries, diagrams, or analysis outputs.

AI can accelerate requirements work, but the Requirements Engineer remains accountable for correctness, meaning, traceability, and stakeholder alignment.

## Contents

- [1. Source Grounding](#1-source-grounding)
- [2. Business Alignment](#2-business-alignment)
- [3. Requirements Quality](#3-requirements-quality)
- [4. Acceptance Criteria Quality](#4-acceptance-criteria-quality)
- [5. Traceability](#5-traceability)
- [6. Risk Review](#6-risk-review)
- [7. Human Review](#7-human-review)
- [8. Confidence Label](#8-confidence-label)
- [Final Decision](#final-decision)
- [Reviewer Notes](#reviewer-notes)

---

## 1. Source Grounding

- [ ] The AI output references the input source or context.
- [ ] Every important statement can be traced back to provided material.
- [ ] The AI clearly separates source-supported facts from assumptions.
- [ ] No unsupported business rules were invented.
- [ ] No stakeholder needs were added without evidence.

---

## 2. Business Alignment

- [ ] The output supports the stated business goal.
- [ ] The business value is clear.
- [ ] The affected stakeholders are identified.
- [ ] The output does not change the original intent.
- [ ] Any trade-offs or decisions are explicitly highlighted.

---

## 3. Requirements Quality

- [ ] Requirements are clear and unambiguous.
- [ ] Requirements are testable.
- [ ] Requirements avoid vague words without a measurable definition (see the [Ambiguity Detector](../prompts/ambiguity-detector.md) for the set to catch).
- [ ] Functional and non-functional requirements are separated where appropriate.
- [ ] Constraints are documented.
- [ ] Assumptions are documented.
- [ ] Open questions are documented.

---

## 4. Acceptance Criteria Quality

- [ ] Acceptance criteria are provided.
- [ ] Acceptance criteria follow a clear structure, for example Given / When / Then.
- [ ] Positive scenarios are covered.
- [ ] Negative scenarios are covered.
- [ ] Boundary conditions are covered.
- [ ] Error handling is covered.
- [ ] Acceptance criteria are realistic and verifiable.

---

## 5. Traceability

- [ ] Each requirement has a unique ID.
- [ ] Each requirement links to a business objective.
- [ ] Each requirement links to source material.
- [ ] Each requirement can be linked to test cases.
- [ ] Decisions and assumptions are traceable.
- [ ] Changes can be reviewed through version control.

---

## 6. Risk Review

- [ ] Security risks were considered.
- [ ] Privacy risks were considered.
- [ ] Compliance risks were considered.
- [ ] Operational risks were considered.
- [ ] User experience risks were considered.
- [ ] Implementation risks were considered.
- [ ] Dependencies were identified.

---

## 7. Human Review

- [ ] A Requirements Engineer reviewed the output.
- [ ] A relevant subject matter expert reviewed the output.
- [ ] Stakeholder approval is captured where needed.
- [ ] AI-generated assumptions were validated.
- [ ] AI-generated recommendations were challenged.
- [ ] Final acceptance decision is made by a human.

---

## 8. Confidence Label

Assign one label to the AI output.

| Label | Meaning | Action |
|---|---|---|
| Source Supported | Directly supported by provided material | May be used after review |
| Inferred | Reasonable interpretation, but not explicit | Requires human validation |
| Missing Evidence | Not supported by provided material | Do not accept without stakeholder confirmation |
| Contradictory | Conflicts with source material or other requirements | Resolve before use |

---

## Final Decision

| Decision | Select |
|---|---|
| Accept | [ ] |
| Accept with changes | [ ] |
| Reject | [ ] |
| Needs stakeholder clarification | [ ] |

---

## Reviewer Notes

```text
Add notes here.
```
