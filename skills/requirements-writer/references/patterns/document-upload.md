# Document Upload Requirement Pattern

## Contents

- Purpose
- Generic Requirement
- Example Requirement
- Core Requirement Fields
- Example Functional Requirements
- Acceptance Criteria
- Non-Functional Considerations
- AI Review Prompt

## Purpose

Use this pattern when users need to upload files into a system for review, storage, processing, validation, or evidence collection.

Document upload requirements often require careful attention to file types, size limits, security scanning, metadata, access rights, auditability, and user feedback.

---

## Generic Requirement

The system shall allow authorized users to upload documents that meet the defined file type, file size, security, and metadata requirements.

---

## Example Requirement

The system shall allow customers to upload PDF documents up to 20 MB as supporting evidence for an application.

---

## Core Requirement Fields

| Field | Description |
|---|---|
| File Type | Which formats are allowed? |
| File Size | What is the maximum file size? |
| User Role | Who is allowed to upload? |
| Business Object | What is the document linked to? |
| Metadata | What information is captured with the file? |
| Validation | What checks are performed? |
| Storage | Where/how is the file stored? |
| Access Control | Who can view, replace, or delete the file? |
| Audit Trail | What upload events are logged? |
| Retention | How long is the file kept? |

---

## Example Functional Requirements

### FR-001: Upload Document

The system shall allow authorized users to upload a document to a business record.

---

### FR-002: Validate File Type

The system shall accept only configured file types.

---

### FR-003: Validate File Size

The system shall reject files that exceed the configured maximum file size.

---

### FR-004: Scan Uploaded Files

The system shall scan uploaded files for malicious content before making them available to other users.

---

### FR-005: Store Document Metadata

The system shall store document metadata including file name, file type, file size, upload timestamp, uploading user, and related business record ID.

---

### FR-006: Record Upload Audit Event

The system shall record an audit event when a document is uploaded, replaced, downloaded, or deleted.

---

## Acceptance Criteria

### AC-01: Successful Upload

Given an authorized user selects a valid PDF file

And the file size is below the configured maximum

When the user uploads the file

Then the system shall attach the document to the selected business record.

---

### AC-02: Invalid File Type

Given an authorized user selects a file type that is not allowed

When the user attempts to upload the file

Then the system shall reject the file

And display a clear validation message.

---

### AC-03: File Too Large

Given an authorized user selects a file that exceeds the maximum file size

When the user attempts to upload the file

Then the system shall reject the file

And explain the maximum allowed size.

---

### AC-04: Security Scan Failure

Given an uploaded file fails the security scan

When the scan result is received

Then the system shall block access to the file

And record the failed scan result.

---

### AC-05: Metadata Capture

Given a document is uploaded successfully

When the upload is completed

Then the system shall store the required metadata for the document.

---

### AC-06: Audit Trail

Given a document is uploaded, replaced, downloaded, or deleted

When the action is completed

Then the system shall record the action in the audit trail.

---

## Non-Functional Considerations

- Upload performance should be acceptable for expected file sizes.
- Users should receive clear feedback during long uploads.
- Sensitive documents should be protected by role-based access control.
- Files should not be available until required validations are complete.
- Document retention rules should be defined.
- Failed uploads should not create incomplete or misleading records.

---

## AI Review Prompt

```text
Act as a Senior Requirements Engineer.

Review the following document upload requirement.

Check for:

1. Allowed file types
2. Maximum file size
3. Upload permissions
4. Validation rules
5. Virus or malware scanning
6. Metadata requirements
7. Storage requirements
8. Access control
9. Audit trail
10. Retention rules
11. User feedback and error handling
12. Ambiguous wording

Return findings as a markdown table with:

- Issue
- Risk
- Suggested improvement
- Severity
```
