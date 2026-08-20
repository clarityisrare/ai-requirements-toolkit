# Worked example — one acceptance criterion to test cases

This shows the table shape `references/test-case-generator.md` asks for: one
acceptance criterion turned into concrete cases, each carrying the eight fields and
naming the criterion it verifies. Adapt the columns to your tracker; keep the
**Linked AC** column so coverage stays traceable.

## Source criterion

- **AC-12** — Given a user has entered an incorrect password 4 times, when they
  enter an incorrect password a 5th time, then the account is locked for 15 minutes
  and a lockout notice is shown.

## Test cases

| Test ID | Linked AC | Title | Preconditions | Steps | Test data | Expected result | Type |
|---|---|---|---|---|---|---|---|
| TC-12-01 | AC-12 | Account locks on 5th consecutive wrong password | Account is active; 4 failed attempts already recorded | 1. Open login. 2. Enter valid username + wrong password. 3. Submit. | username `jo@acme.io`, password `wrong-5` | Login rejected; account locked for 15 min; lockout notice shown | Positive |
| TC-12-02 | AC-12 | 4th wrong password does not lock the account | Account is active; 3 failed attempts already recorded | 1. Open login. 2. Enter valid username + wrong password. 3. Submit. | username `jo@acme.io`, password `wrong-4` | Login rejected; account stays unlocked; 1 attempt remaining | Boundary |
| TC-12-03 | AC-12 | Correct password is refused while the account is locked | Account locked less than 15 min ago | 1. Open login. 2. Enter valid username + correct password. 3. Submit. | username `jo@acme.io`, password `correct` | Login refused with lockout notice; account stays locked until the window elapses | Negative |
