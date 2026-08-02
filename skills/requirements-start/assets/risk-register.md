# Risk Register

Track risks to the requirements and the delivery — what could go wrong, how likely and how
bad, and who owns the response. Review it regularly; a risk register that is never updated is
just a document.

Record only risks the request or the conversation actually surfaces. Do not invent an owner,
a likelihood, or an impact you cannot support — leave the field **Open** rather than assigning
a name or a rating that nobody agreed to.

---

## Scoring

- **Likelihood:** Low / Medium / High
- **Impact:** Low / Medium / High
- **Severity:** derive from Likelihood × Impact (High if either is High and the other is at least Medium)
- **Response:** Avoid / Reduce / Transfer / Accept

---

## Structure

| ID | Risk | Category | Likelihood | Impact | Severity | Response | Owner | Status |
|---|---|---|---|---|---|---|---|---|
| | | | | | | | | |

### [Risk ID]

- **Trigger / early warning:**
- **Mitigation actions:**
- **Contingency if it occurs:**

## Change log

| Date | Risk | Change | Author |
|---|---|---|---|
| | | | |

---

## Worked example

For an upload-and-approval domain, an early register might read:

| ID | Risk | Category | Likelihood | Impact | Severity | Response | Owner | Status |
|---|---|---|---|---|---|---|---|---|
| RSK-001 | Uploaded malware reaches internal users | Security | Medium | High | High | Reduce — scan before access | Security Lead | Open |
| RSK-002 | Ambiguous requirements cause rework | Delivery | High | Medium | High | Reduce — ambiguity review | BA | Open |
| RSK-003 | External payment API downtime blocks approvals | Integration | Low | High | Medium | Reduce — retry + queue | Tech Lead | Open |
