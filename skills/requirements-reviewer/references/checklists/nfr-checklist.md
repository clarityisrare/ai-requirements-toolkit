# Non-Functional Requirements Checklist

Functional requirements describe *what* a system does. This checklist makes sure you have
also considered *how well* it must do it. Not every category applies to every feature — mark
the ones that do, and give each a **measurable** target.

Companion prompt: [NFR Generator](../prompts/nfr-generator.md).

---

## Performance

- [ ] Response time target defined (e.g. 95th percentile under 500 ms)
- [ ] Throughput target defined (requests or transactions per second)
- [ ] Target stated at a defined data volume and load

## Scalability

- [ ] Expected and peak load documented
- [ ] Growth expectation documented
- [ ] Behavior under overload defined

## Availability & Reliability

- [ ] Availability target defined (e.g. 99.9%)
- [ ] Recovery expectations defined (RTO / RPO)
- [ ] Behavior on dependency failure defined

## Security

- [ ] Authentication requirements defined
- [ ] Authorization / access control defined
- [ ] Data-in-transit protection defined
- [ ] Data-at-rest protection defined

## Privacy & Data Protection

- [ ] Personal / regulated data identified
- [ ] Retention and deletion rules defined
- [ ] Consent and lawful basis considered where relevant

## Usability & Accessibility

- [ ] Accessibility standard named (e.g. WCAG 2.2 AA)
- [ ] Key user tasks have a defined ease-of-use expectation
- [ ] Error messages are specified as clear and actionable

## Maintainability & Observability

- [ ] Logging requirements defined
- [ ] Monitoring and alerting defined
- [ ] Configuration vs code changes distinguished

## Compatibility & Compliance

- [ ] Supported browsers / devices / platforms defined
- [ ] Interoperability requirements defined
- [ ] Applicable legal / regulatory standards identified

---

## Quality gate

- [ ] Every applicable NFR has a **measurable** target (a number or condition, not "fast",
      "secure", or "user friendly")
- [ ] Every target states how it will be verified
- [ ] Non-applicable categories are explicitly marked "N/A", not left blank
