# Glossary Builder Prompt

Use this prompt to extract a shared glossary of terms from requirements, notes, or
transcripts. A common vocabulary is one of the cheapest ways to prevent ambiguity and
rework across a team.

Review the output with a domain expert, then keep the glossary in one place and link
requirements to it. See the companion [glossary template](../templates/glossary.md).

---

## Prompt

```text
Act as a Senior Requirements Engineer building a domain glossary.

Extract and define the important terms from the material below.

Material:
[PASTE REQUIREMENTS / NOTES / TRANSCRIPT HERE]

Known domain or context:
[PASTE DOMAIN CONTEXT HERE]

For each term, provide:

- Term
- Definition (plain language, one or two sentences)
- Synonyms or aliases seen in the material
- Example usage
- Related terms
- Status: Confirmed / Needs SME confirmation / Conflicting definitions found

Rules:
- Prefer definitions grounded in the material. If you must infer, mark the term
  "Needs SME confirmation".
- Flag terms that are used with more than one meaning as "Conflicting definitions found"
  and list the conflicting uses.
- Do not invent domain concepts that are not present in the material.
- Be concise: no preamble and no restating the material. Include only terms the material actually uses — omit anything not present rather than padding. One term per row; no repetition.

Return the result as a markdown table, sorted alphabetically by term.
```
