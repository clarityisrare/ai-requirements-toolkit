# Run Manifest

```yaml
run_id: 2026-08-19-1432-emir-vs-fmia104-scope
created: 2026-08-19T14:32:00Z
grounding_mode: 1
as_of_date: 2026-08-19
corpus_path: ./corpus
```

## Request

**Question:** <verbatim>

**Fact pattern:** <entity type, jurisdiction of establishment, counterparty type,
product, venue, client category — whatever was given>

**Assumptions recorded:** <facts the user did not supply that were assumed, or
"none">

**Classification:** `REGULATORY_COMPARISON`

## Agents engaged

| Agent | Ran | Output | REQ | INT | AMB | RSK | GAP |
|---|---|---|---|---|---|---|---|
| `sme-emir` | yes | `10-sme-emir.md` | 6 | 2 | 1 | 2 | 0 |
| `sme-fmia-art-104` | yes | `10-sme-fmia-art-104.md` | 5 | 1 | 2 | 1 | 1 |

## Stages

| Stage | Status | Output | Note |
|---|---|---|---|
| `reg-comparison` | ran | `20-comparison.md` | 9 findings |
| `reg-convergence` | skipped | — | No implementation or operating model question asked |
| `reg-output-quality` | ran | `40-response.md` | Overall confidence MEDIUM |
| `reg-executive-output` | skipped | — | No executive audience requested |

## Open items carried into the output

**Unresolved conflicts:** `CMP-FND-004` — SME positions on intragroup treatment
are incompatible; needs specialist review.

**Evidence gaps:** `FMIA104-GAP-001` — FINMA guidance on <point> could not be
retrieved under the grounding mode in force.

**Coverage gaps:** none.

## Verification

- [ ] Every downstream ID resolves to an upstream finding
- [ ] Conflicts and gaps survive into `40-response.md`
- [ ] Jurisdictions separated throughout
- [ ] Sources attributed with tags and dates
