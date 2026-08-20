# Worked Example — "Who reports, EMIR or FMIA?"

An end-to-end run, abridged, showing what each stage produces and — more usefully
— what each stage refuses to do.

> **The question.** *"We're a Swiss bank with an EU branch. For an OTC interest
> rate swap with an EU non-financial counterparty below the clearing threshold —
> who has to report, and can we handle both regimes on one platform?"*

---

## Stage 1 — Orchestrator

**Missing facts, asked before dispatch.** Where is the swap booked? Is the EU
branch a separate legal entity or a branch of the Swiss entity? Is the NFC
established in the EU? The answers change the analysis, so guessing them wastes
the entire run.

*Answered: booked in Zurich, EU branch is a branch of the Swiss entity, NFC- is
EU-established.*

**Classification:** `REGULATORY_COMPARISON` + `CONVERGENCE_ASSESSMENT` — the
question has two halves and the second one ("one platform") is what pulls the
convergence stage in.

**Routing:** `sme-emir` and `sme-fmia-art-104`, in parallel. Not
`sme-fmia-art-39` — Art. 39 is trading venue transaction reporting, and this is a
trade repository question. Not `sme-mifir-transaction-reporting` — an OTC swap
with no venue execution raises a different obligation than the one asked about.

Two SMEs, not six. The restraint is the point.

---

## Stage 2 — SMEs (parallel, isolated)

Neither knows the other is running.

**`10-sme-emir.md`** (extract)

> **EMIR-REQ-001** · `REPORTING_PARTY` · Evidence: STRONG
> Both counterparties must ensure the details of their derivative contract are
> reported. The obligation is **dual-sided**.
> Source: EMIR Art. 9(1) [CORPUS] `corpus/eu/emir.md`
>
> **EMIR-REQ-002** · `REPORTING_PARTY / DELEGATED_REPORTING` · Evidence: STRONG
> Where an FC faces an NFC below the clearing threshold, the FC is responsible
> and legally liable for reporting on behalf of both.
> Source: EMIR Art. 9(1a) [CORPUS] `corpus/eu/emir.md`
>
> **EMIR-AMB-001**
> Whether the Swiss entity is an FC for these purposes turns on third-country
> treatment, which depends on facts not supplied. The position below is
> conditional.

**`10-sme-fmia-art-104.md`** (extract)

> **FMIA104-REQ-002** · `REPORTING_PARTY / REPORTING_CASCADE` · Evidence: STRONG
> The obligation is **single-sided**, allocated by cascade: CCP where centrally
> cleared; the FC where facing an NFC; the non-small counterparty where facing a
> small one; otherwise the selling counterparty unless agreed otherwise.
> Source: FinfraG Art. 104 [CORPUS] `corpus/ch/finfrag.md`

Note what neither did: neither mentioned the other regime, and neither said which
obligation "wins". They were not asked, and they could not see each other.

---

## Stage 3 — Comparison

> **CMP-FND-001** · `REPORTING_PARTY` · **CONFIRMED_DIFFERENCE** · Evidence: STRONG
>
> - **EU** (`EMIR-REQ-001`): dual-sided obligation; each counterparty must ensure
>   its side is reported.
> - **Switzerland** (`FMIA104-REQ-002`): single-sided obligation allocated by
>   cascade.
> - **Basis:** both positions rest on Tier 1 text, cited pinpoint. The difference
>   is structural, not a drafting variation.
> - **What this does not say:** this does not determine which obligation applies
>   to this entity, nor whether both apply simultaneously. That depends on the
>   third-country and branch analysis flagged in `EMIR-AMB-001`.
>
> **CMP-FND-002** · `REPORTING_PARTY` · **PARTIAL_ALIGNMENT** · Evidence: MODERATE
> `EMIR-REQ-002` ↔ `FMIA104-REQ-002`. Both allocate the obligation to the
> financial counterparty when facing a non-financial one. EMIR attaches legal
> liability for the counterparty's data; the Swiss cascade allocates the duty
> without the equivalent liability construct being identified in the SME
> findings.
>
> **Convergence escalation flag:** both regimes depend on counterparty
> categorisation data and on UTI generation. Shared data dependency — worth a
> convergence assessment.

Both regimes require a report of the same swap, and it would be easy to write
"the obligation is broadly the same". The comparison stage exists to stop that
sentence being written.

---

## Stage 4 — Convergence

> **CNV-CAP-001 — Counterparty Categorisation** · `HIGH_CONVERGENCE`
> Supporting: `CMP-FND-002`
>
> | Dimension | Assessment | Basis |
> |---|---|---|
> | Business process | Convergent | `CMP-FND-002` |
> | Data | Convergent | `CMP-FND-002` |
> | Technology | Convergent | — |
> | Control | Partially convergent | `CMP-FND-001` |
> | Governance | Convergent | — |
> | Operating model | Convergent | — |
> | Reporting production | **Divergent** | `CMP-FND-001` |
>
> Capped at `HIGH` rather than `EXACT` by reporting production: a single-sided
> cascade and a dual-sided obligation cannot share a submission decision.
>
> **CNV-LOC-001** · `CONTROL_LOCALIZATION` · Switzerland
> A cascade-determination control is needed on the Swiss side with no EU
> equivalent, since EMIR does not require the firm to determine which party
> reports.
>
> **Residual fragmentation**
> Submission logic remains regime-specific. Counterparty data, instrument data
> and UTI generation converge; the decision of *whether and by whom to submit*
> does not.

The answer to "can we run one platform?" is *mostly yes, and here is precisely
where it breaks* — which is more useful than either a yes or a no.

---

## Stage 5 — Output & Quality

Assembles the comparison structure, keeps the Swiss and EU sections apart, and
assigns confidence:

| Dimension | Level | Rationale |
|---|---|---|
| Regulatory | MEDIUM | Both positions are Tier 1 and STRONG, but `EMIR-AMB-001` leaves third-country treatment unresolved, and the answer depends on it |
| Comparison | HIGH | The structural difference is visible in the legal text on both sides |
| Convergence | MEDIUM | Control and reporting-production assessments rest partly on interpretation |
| **Overall** | **MEDIUM** | Floored by regulatory confidence; the unresolved third-country point is material to who reports |

The ID audit removes a sentence from the draft that read *"the Swiss entity
should register with an EU trade repository"* — no upstream finding said it, and
it is a recommendation besides.

---

## Stage 6 — Executive brief

> **Bottom line.** Both regimes require this swap to be reported, but they
> allocate the duty differently — Switzerland to one party by cascade, the EU to
> both. Counterparty data, instrument data and UTI generation can be shared
> across a single platform; the submission decision cannot. One question is
> unresolved and blocks a firm answer on who reports: whether our Swiss entity
> is treated as a financial counterparty for EMIR third-country purposes. That
> needs legal input before the reporting design is fixed.

Note what the executive brief keeps: the unresolved question, in the bottom line,
where a summary written for comfort would have buried it.

---

## What the run cost

Two SME subagents in parallel, four sequential stages, one clarifying exchange
before dispatch. Three SMEs and two stages were correctly not run.
