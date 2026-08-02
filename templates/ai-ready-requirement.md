# AI-Ready Requirement Template

A single, traceable requirement carrying its source and confidence, so the next
reader knows what is grounded and what still needs confirming. Copy the skeleton,
fill only what the input supports, and route the rest to **Open Questions** —
never invent an ID, a limit, a source, or a traceability link.

---

## Template

```markdown
# Requirement

## ID
REQ-NNN

## Title
[Short noun phrase naming the behavior]

## Business Goal
[Why this matters — the business outcome it serves]

## Stakeholders
- [Role or group affected; add one per line]

## Requirement Statement
The system shall [one testable behavior].

## Constraints
- [Known limit, rule, or boundary the input supplied — omit if none known]

## Acceptance Criteria
### AC-01
Given [context]
When [action]
Then [expected result]

## Traceability
Business Requirement: [BR-NNN or Open]
Epic: [EPIC-NNN or Open]
Risk: [RSK-NNN or Open]

## AI Readiness
### Source
[Where this came from: interview, document, ticket — or "Missing evidence"]

### Confidence
[Source Supported | Inferred | Missing Evidence]

### Open Questions
- [Anything the input did not settle]
```

---

## Filled example

```markdown
# Requirement

## ID
REQ-001

## Title
Customer Uploads Documents

## Business Goal
Enable customers to provide documents required for account opening.

## Stakeholders
- Customer
- Operations Team
- Compliance Team

## Requirement Statement
The system shall allow customers to upload PDF documents up to 20 MB.

## Constraints
- PDF only
- Maximum 20 MB
- Virus scanning mandatory

## Acceptance Criteria
### AC-01
Given a customer selects a PDF
When the file size is less than 20 MB
Then the upload shall succeed

### AC-02
Given a customer uploads an executable file
When the system validates the file
Then the upload shall be rejected

## Traceability
Business Requirement: BR-001
Epic: EPIC-003
Risk: RSK-004

## AI Readiness
### Source
Stakeholder Interview 2026-05-20

### Confidence
Source Supported

### Open Questions
- Retention period after account closure?
```
