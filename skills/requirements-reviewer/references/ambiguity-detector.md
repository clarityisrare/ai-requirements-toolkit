# Ambiguity Detector Prompt

Use this prompt to surface vague or subjective wording in a requirement before it reaches development or QA.

---

## Prompt

```text
Analyze the following requirement.

Find words and phrases that may be interpreted in more than one way.

Examples:

- Fast
- Easy
- Appropriate
- Secure
- Flexible
- Efficient
- User-friendly

Return a markdown table with:

- Term
- Reason for ambiguity
- Recommended rewrite
```
