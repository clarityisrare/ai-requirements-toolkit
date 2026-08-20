# Finding IDs and Traceability

Every material finding gets a stable ID at the moment it is created. Without
this, nothing downstream can point back to anything, and "traceability" becomes
a claim rather than a property.

## ID format

```
<DOMAIN>-<KIND>-<NNN>
```

**Domain codes** (fixed — never invent new ones):

| Code | Agent |
|---|---|
| `FMIA39` | `sme-fmia-art-39` |
| `FMIA104` | `sme-fmia-art-104` |
| `EMIR` | `sme-emir` |
| `MIFIR` | `sme-mifir-transaction-reporting` |
| `MIFID2` | `sme-mifid2-client-classification` |
| `FINSA` | `sme-finsa-client-segmentation` |
| `CMP` | `reg-comparison` |
| `CNV` | `reg-convergence` |

**Kind codes:**

| Code | Meaning | Created by |
|---|---|---|
| `REQ` | A requirement supported by an identified source | SME |
| `INT` | An interpretation — the SME's reasoning, not an explicit source | SME |
| `AMB` | An ambiguity or open question in the official material | SME |
| `RSK` | An implementation or compliance risk | SME |
| `GAP` | An evidence gap — something that could not be established | any stage |
| `FND` | A comparison finding (a pairing plus its classification) | `reg-comparison` |
| `CAP` | A convergence capability assessment | `reg-convergence` |
| `LOC` | A localisation requirement | `reg-convergence` |

Numbering starts at `001` per domain per kind, per run. IDs are never reused,
renumbered, or merged once written.

Examples: `EMIR-REQ-003`, `FMIA104-AMB-001`, `CMP-FND-007`, `CNV-CAP-002`,
`CNV-LOC-004`.

## The traceability contract

- **SMEs** assign IDs to every requirement, interpretation, ambiguity, risk and
  gap they emit.
- **`reg-comparison`** never restates a requirement in its own words without
  citing the SME ID it came from. Each comparison finding names the upstream IDs
  on both sides:
  `CMP-FND-007: EMIR-REQ-003 ↔ FMIA104-REQ-005 — PARTIAL_ALIGNMENT`.
  A one-to-many pairing is written with all IDs listed:
  `EMIR-REQ-003 ↔ {FMIA104-REQ-005, FMIA104-REQ-009}`.
- **`reg-convergence`** cites the `CMP-FND-*` IDs that support each capability
  assessment and each localisation requirement.
- **`reg-output-quality`** carries IDs through into the business response. They
  may be moved into a traceability appendix rather than the body, but they are
  never dropped.
- **`reg-executive-output`** may omit IDs from the narrative, but its
  traceability section must still let a reader walk any statement back to a
  source.

## The rule that makes it work

**If a downstream stage cannot name the upstream ID behind a statement, that
statement does not belong in the output.** It is either an invention, or it is a
new finding that should have been raised by an SME. Either way, it gets removed
or converted into an explicit `GAP`.

## Traceability appendix

Every terminal output ends with a table:

| Statement / section | Supporting IDs | Origin agent | Evidence strength |
|---|---|---|---|
| Reporting obligation is single-sided under FMIA | `FMIA104-REQ-002` | `sme-fmia-art-104` | STRONG |
| Dual-sided under EMIR | `EMIR-REQ-001` | `sme-emir` | STRONG |
| Difference is structural, not cosmetic | `CMP-FND-001` | `reg-comparison` | STRONG |
