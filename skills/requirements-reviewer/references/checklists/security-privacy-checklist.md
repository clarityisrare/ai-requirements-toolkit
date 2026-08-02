# Security & Privacy Requirements Checklist

Use this checklist to make sure security and privacy are considered while requirements are
written — not bolted on after a system is built. It is a prompt for questions, not a
substitute for a formal security review or a Data Protection Impact Assessment.

---

## Authentication & Authorization

- [ ] How users prove who they are is defined
- [ ] What each role may do is defined (see the Access Control pattern in the requirements-writer skill)
- [ ] Access is denied by default (least privilege)
- [ ] Authorization is enforced server-side, not only in the UI
- [ ] Session and token handling is considered (expiry, revocation)

## Data Protection

- [ ] Sensitive and personal data is identified
- [ ] Data in transit is protected (e.g. TLS)
- [ ] Data at rest is protected where required
- [ ] Data is minimized to what is actually needed
- [ ] Sensitive data is masked in logs, exports, and error messages

## Privacy

- [ ] Lawful basis / consent is considered where personal data is processed
- [ ] Retention and deletion rules are defined
- [ ] Data subject rights (access, deletion, correction) are considered
- [ ] Data sharing with third parties is documented

## Input & Output

- [ ] Input validation rules are defined
- [ ] File uploads are scanned and constrained (see the Document Upload pattern in the requirements-writer skill)
- [ ] Error messages avoid leaking sensitive detail

## Auditing & Monitoring

- [ ] Security-relevant events are logged (see the Audit Trail pattern in the requirements-writer skill)
- [ ] Failed access attempts are recorded
- [ ] Monitoring / alerting for suspicious activity is considered

## Resilience

- [ ] Behavior under abuse or overload is considered
- [ ] Backups and recovery expectations are defined
- [ ] Third-party dependency risks are considered

---

## Result

- [ ] No open high-severity security or privacy concerns
- [ ] Open concerns are logged and assigned an owner
- [ ] A security / privacy specialist has reviewed where required
