# Non-Functional Requirement

## ID

NFR-001

---

## Category

Performance

---

## Related Feature / Requirement

REQ-001 — Customer Uploads Documents

---

## Requirement Statement

The document upload shall complete within a defined time for files up to the maximum allowed
size, under expected load.

---

## Measurable Target

- 95th percentile upload time under 3 seconds for a 20 MB file
- Measured at 50 concurrent uploads

---

## Rationale

Slow uploads cause customers to abandon the application, directly affecting completion rates.

---

## Verification Method

Load test with 50 concurrent 20 MB uploads; record the 95th percentile completion time.

---

## Assumptions

- Typical customer connection is at least 10 Mbps.

---

## Priority

Must have

---

## Status

Draft / Under review / Approved
