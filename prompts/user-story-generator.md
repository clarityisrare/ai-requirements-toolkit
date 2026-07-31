# User Story Generator Prompt

Use this prompt to turn a feature idea, requirement, or business need into well-formed user
stories that pass an INVEST review.

The output should be reviewed by a Product Owner or Requirements Engineer, and validated with
stakeholders, before it enters a backlog. See the companion
[INVEST checklist](../checklists/user-story-quality.md).

---

## Prompt

```text
Act as a Senior Requirements Engineer and Product Owner.

Turn the input below into clear, INVEST-compliant user stories.

Feature or need:
[PASTE FEATURE OR NEED HERE]

Business Goal:
[PASTE BUSINESS GOAL HERE]

Known Users / Roles:
[PASTE ROLES HERE]

Known Constraints:
[PASTE CONSTRAINTS HERE]

For each user story, produce:

- Story ID
- Title
- Story in the form: As a [role], I want [capability], so that [benefit]
- 3 to 6 acceptance criteria in Given / When / Then format
- INVEST notes (flag anything that is not Independent, Negotiable, Valuable, Estimable,
  Small, or Testable)
- Assumptions (clearly labeled)
- Open questions

Rules:
- Do not invent business rules or user needs that are not supported by the input.
- Split stories that are too large; note where you split and why.
- Prefer user value over implementation detail.
- List anything missing under "Open Questions".
- Be concise: no preamble, and do not restate the input. Produce the fewest stories that fully cover the need — one section per story, no padding or repetition.

Return the result as markdown, one section per story.
```
