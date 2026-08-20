# SME Finding Quality Checklist

Run against any `10-sme-*.md` before it goes downstream.

## Sourcing
- [ ] Every requirement carries a pinpoint citation — article, paragraph, letter;
      RTS field number; Q&A number; circular margin number
- [ ] Every citation carries a tag: `[CORPUS]`, `[RETRIEVED <date>]`,
      `[SECONDARY]`, or `[UNVERIFIED]`
- [ ] No `[SECONDARY]` source used where an official source answers the point
- [ ] No requirement rests on a bare regime name ("EMIR requires…")
- [ ] Grounding mode honoured — Mode 2 has no unretrieved citations; Mode 3 has
      nothing outside the corpus

## Separation
- [ ] Legal text, regulator guidance, interpretation and market practice are
      separately labelled
- [ ] Every interpretation is an `INT` finding, not a `REQ`
- [ ] No market practice presented as a regulatory expectation
- [ ] Nothing said about any regime other than this agent's own

## Classification
- [ ] Every requirement has exactly one core type from the shared taxonomy
- [ ] Domain qualifiers used where they add precision, and are valid values
- [ ] `OTHER` used only with a stated reason

## Traceability
- [ ] Every finding has a unique ID with the correct domain prefix
- [ ] IDs are sequential within kind and not reused
- [ ] Evidence strength assigned to every requirement and interpretation

## Completeness
- [ ] The question actually asked is answered, and anything out of scope is named
- [ ] Ambiguities registered rather than resolved by assumption
- [ ] Evidence gaps registered with what would close them
- [ ] Implementation risks tied to specific requirements
- [ ] Operational implications stated as facts about this regime, with no
      evaluation of shareability with another

## Temporal
- [ ] As-of date stated
- [ ] Regime version stated, including relevant amendments
- [ ] Pending changes flagged with status and timing, or "none identified"
- [ ] Nothing with a future application date presented as current law

## The honesty test
- [ ] Every uncertain point reads as uncertain
- [ ] Nothing was asserted because it sounded right
