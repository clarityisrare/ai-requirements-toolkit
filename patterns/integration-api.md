# Integration / API Requirement Pattern

## Purpose

Use this pattern when your system must exchange data with another system — inbound or outbound
APIs, webhooks, file feeds, or message queues.

Integration requirements fail quietly when teams skip error handling, retries, idempotency,
versioning, and what happens when the other system is unavailable.

---

## Generic Requirement

The system shall exchange the required data with the external system reliably, handle
failures predictably, and record the outcome of each exchange.

---

## Example Requirement

The system shall send each approved request to the payment system via its REST API, retry on
transient failure, and mark the request as failed if it cannot be delivered within the agreed
window.

---

## Core Requirement Fields

| Field | Description |
|---|---|
| Direction | Inbound, outbound, or bidirectional? |
| Trigger | What starts the exchange (event, schedule, request)? |
| Data | What data is exchanged, and in what format? |
| Protocol | REST, webhook, file, message queue? |
| Authentication | How are the systems authenticated to each other? |
| Idempotency | How are duplicate messages handled safely? |
| Error Handling | What happens on failure, timeout, or rejection? |
| Retry Policy | How many retries, with what backoff? |
| Ordering | Does message order matter? |
| Versioning | How are contract changes managed? |
| Monitoring | How are failures detected and surfaced? |

---

## Example Functional Requirements

### FR-001: Send on Event

The system shall send the defined data to the external system when the trigger event occurs.

---

### FR-002: Authenticate the Exchange

The system shall authenticate each request to the external system using the agreed mechanism.

---

### FR-003: Handle Failure

The system shall detect failed exchanges and apply the defined retry policy.

---

### FR-004: Ensure Idempotency

The system shall ensure that re-sending the same message does not create duplicate records in
the external system.

---

### FR-005: Record Outcome

The system shall record the outcome of each exchange, including success, failure, and retry
attempts.

---

## Acceptance Criteria

### AC-01: Successful Exchange

Given a request is approved

When it is sent to the payment system

Then the payment system shall acknowledge receipt and the request shall be marked as sent.

---

### AC-02: Transient Failure Retry

Given the external system returns a transient error

When the exchange fails

Then the system shall retry according to the defined policy.

---

### AC-03: Permanent Failure

Given the external system rejects the message as invalid

When the rejection is received

Then the system shall mark the exchange as failed and make it visible for operational review.

---

### AC-04: Idempotent Delivery

Given the same message is delivered twice

When the external system processes it

Then only one record shall result.

---

### AC-05: Outcome Recorded

Given any exchange is attempted

When it completes or fails

Then the system shall record the outcome and attempt count.

---

## Non-Functional Considerations

- The integration should not block the user action that triggers it, where asynchronous handling is possible.
- The system should remain stable when the external system is slow or unavailable.
- Sensitive data in transit should be protected (e.g. TLS) and minimized to what is needed.
- Contract changes should be versioned so existing consumers are not broken.
- Throughput and rate limits of the external system should be respected.
- Failures should be observable through monitoring and alerting, not discovered by users.

---

## AI Review Prompt

```text
Act as a Senior Requirements Engineer with integration experience.

Review the following integration / API requirement.

Check for:

1. Direction and trigger of the exchange
2. Data and format exchanged
3. Protocol (REST, webhook, file, queue)
4. Authentication between systems
5. Idempotency / duplicate handling
6. Error handling for transient and permanent failures
7. Retry policy and backoff
8. Message ordering requirements
9. Contract versioning
10. Behavior when the external system is unavailable
11. Monitoring and alerting
12. Security of data in transit
13. Ambiguous wording

Return findings as a markdown table with:

- Issue
- Risk
- Suggested improvement
- Severity
```
