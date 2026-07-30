# Requirement

## ID

REQ-001

---

## Title

Customer Uploads Documents

---

## Business Goal

Enable customers to provide documents required
for account opening.

---

## Stakeholders

- Customer
- Operations Team
- Compliance Team

---

## Requirement Statement

The system shall allow customers to upload
PDF documents up to 20 MB.

---

## Constraints

- PDF only
- Maximum 20 MB
- Virus scanning mandatory

---

## Acceptance Criteria

### AC-01

Given a customer selects a PDF

When the file size is less than 20 MB

Then the upload shall succeed

---

### AC-02

Given a customer uploads an executable file

When validation is performed

Then the upload shall be rejected

---

## Traceability

Business Requirement: BR-001

Epic: EPIC-003

Risk: RSK-004

---

## AI Readiness

### Source

Stakeholder Interview 2026-05-20

### Confidence

Source Supported

### Open Questions

-
