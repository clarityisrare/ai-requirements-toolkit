# Comparison Integrity Checklist

Run against `20-comparison.md` before handing off.

## Inputs
- [ ] At least two SME files, covering distinct domains
- [ ] Nothing compared that no SME finding supports
- [ ] No regulation opened, retrieved, or interpreted by this stage

## Pairing
- [ ] Pairs share a core type
- [ ] Matched on regulatory concept and objective, not on similar wording
- [ ] One-to-many pairings list every ID on both sides
- [ ] Every unmatched requirement resolved as `NO_EXACT_EQUIVALENT`, not dropped

## Classification
- [ ] Exactly one classification per finding, from the permitted set
- [ ] `CONFIRMED_*` used only where both sides rest on explicit SME evidence
- [ ] `INTERPRETED_DIFFERENCE` used where the difference rests on interpretation
- [ ] `INSUFFICIENT_EVIDENCE` used rather than a guess
- [ ] Evidence strength assigned, and not confused with confidence
- [ ] No confidence rating anywhere in the file

## The five assumptions
- [ ] No pair classified as aligned on wording similarity alone
- [ ] No pair classified as different on wording difference alone
- [ ] No statement that alignment implies convergence
- [ ] No statement that difference prevents convergence
- [ ] No inference from an SME's silence about what a regime requires

## Preservation
- [ ] Both positions recorded in full for every conflict
- [ ] No conflict resolved, ranked, or averaged
- [ ] Jurisdiction labels on every statement
- [ ] Source lists not merged across jurisdictions
- [ ] SME defects described in Consistency Observations, not silently repaired

## Boundaries
- [ ] No operating model, architecture, system or platform evaluation
- [ ] No convergence assessment — flags only, with the trigger named
- [ ] No statement of legal equivalence
- [ ] Operational implications recorded and compared, not evaluated

## Output
- [ ] Summary table present and complete
- [ ] Every detailed finding names the IDs on both sides
- [ ] "What this does not say" stated for material findings
