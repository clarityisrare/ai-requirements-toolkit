# Non-Functional Requirement Template

One NFR with a **measurable** target and a verification method. Copy the skeleton,
and if a target cannot be settled from the input, write "Needs a target" and say
what information is required — never invent a number and present it as agreed.

---

## Template

```markdown
# Non-Functional Requirement

## ID
NFR-NNN

## Category
[Performance | Scalability | Availability | Security | Privacy | Usability |
Maintainability | Compatibility | Compliance | …]

## Related Feature / Requirement
[REQ-NNN — title, or Open]

## Requirement Statement
[How well the system must behave, stated as a condition]

## Measurable Target
- [A number or condition — e.g. "95th percentile under X ms at N concurrent
  users". If unknown, write "Needs a target" and name what is required.]

## Rationale
[Why this target matters — the cost of missing it]

## Verification Method
[How the target will be checked — e.g. a load test and what it measures]

## Assumptions
- [Any inferred input the target depends on; label it clearly]

## Priority
[Must have | Should have | Could have | Won't have]

## Status
Draft / Under review / Approved
```

---

## Filled example

```markdown
# Non-Functional Requirement

## ID
NFR-001

## Category
Performance

## Related Feature / Requirement
REQ-001 — Customer Uploads Documents

## Requirement Statement
The document upload shall complete within a defined time for files up to the
maximum allowed size, under expected load.

## Measurable Target
- 95th percentile upload time under 3 seconds for a 20 MB file
- Measured at 50 concurrent uploads

## Rationale
Slow uploads cause customers to abandon the application, directly affecting
completion rates.

## Verification Method
Load test with 50 concurrent 20 MB uploads; record the 95th percentile
completion time.

## Assumptions
- Typical customer connection is at least 10 Mbps.

## Priority
Must have

## Status
Draft
```
