# Regulatory Domain Map

Which agent owns what, and how the Swiss and EU regimes actually pair up.

## Domain ownership

| Subagent | Regime | Core subject | Primary regulator |
|---|---|---|---|
| `sme-fmia-art-39` | FinfraG / FMIA Art. 39 (+ FinfraV, FinfraV-FINMA, FINMA circulars and guidance on securities transaction reporting) | Reporting duty of Swiss trading venue participants — transaction reporting to the venue's reporting office | FINMA |
| `sme-fmia-art-104` | FinfraG / FMIA Art. 104 (+ FinfraV, FinfraV-FINMA) | Derivatives reporting to a trade repository | FINMA |
| `sme-emir` | EMIR (Reg. (EU) 648/2012), EMIR REFIT, ESMA RTS/ITS/Q&A/Validation Rules | Derivatives reporting to a trade repository, clearing, risk mitigation, reconciliation | ESMA / NCAs |
| `sme-mifir-transaction-reporting` | MiFIR (Reg. (EU) 600/2014) Art. 26, RTS 22/23/24, MiFIR Review (Reg. (EU) 2024/791) | Transaction reporting, instrument reference data | ESMA / NCAs |
| `sme-mifid2-client-classification` | MiFID II (Dir. 2014/65/EU), Del. Reg. 2017/565, Del. Dir. 2017/593 | Client classification, suitability, appropriateness, product governance | ESMA / NCAs |
| `sme-finsa-client-segmentation` | FinSA / FIDLEG (SR 950.1), FinSO / FIDLEV (SR 950.11) | Client segmentation, opting out and opting in, and the conduct duties attaching to each segment | FINMA |

## Functional counterparts — read this before assuming any pairing

The counterpart pairs below are **starting points for comparison, not statements
of legal equivalence**. Confirming or denying equivalence is `reg-comparison`'s
job, on the evidence, per question.

| Swiss | EU | Relationship |
|---|---|---|
| FMIA **Art. 39** — trading venue participant transaction reporting | **MiFIR Art. 26** transaction reporting | Closest functional counterpart. Different reporting recipient (Swiss venue reporting office vs. NCA/ARM), different field sets, different scope triggers. |
| FMIA **Art. 104** — derivatives reporting to a trade repository | **EMIR Art. 9** | Closest functional counterpart. Materially different reporting model: FMIA operates a **single-sided** obligation with a reporting cascade; EMIR is **dual-sided**. |
| **FinSA / FIDLEG Art. 4** — client segmentation | **MiFID II** client classification (Art. 24, Art. 25, Annex II) | Closest functional counterpart, and structurally asymmetric: FinSA draws **three** segments (retail, professional, institutional) on Swiss tests in Swiss francs; MiFID II draws **four** categories (retail, professional per se, elective professional, eligible counterparty). The opt-up routes differ in kind, not only in amount. |

### Correction carried into this toolkit

The originating Copilot Studio agent descriptions paired FMIA Art. 104 with
MiFID II, and MiFID II client classification with FMIA Art. 104. Both are wrong
and would misroute a comparison request. FMIA Art. 104 is trade-repository
derivatives reporting — the counterpart of **EMIR Art. 9**. MiFID II client
classification has no counterpart in FMIA at all; its Swiss analogue sits in
**FinSA (FIDLEG)**, owned by `sme-finsa-client-segmentation`. The table above is
authoritative for routing.

## Comparing client segmentation — the asymmetry to watch

Both sides of client segmentation are covered: `sme-mifid2-client-classification`
for the EU, `sme-finsa-client-segmentation` for Switzerland. A cross-jurisdiction
question here is now two-sided and routes like any other comparison.

What makes this pairing harder than the reporting pairings is that the category
sets are not the same shape. Three Swiss segments do not map onto four EU
categories, and the routes between them differ: FinSA turns opting out on
high-net-worth tests stated in Swiss francs, while MiFID II turns opting up on a
qualitative assessment combined with quantitative tests. A near-identical label
on either side — "professional client" — covers a differently drawn population.

There is a second asymmetry underneath the first. FinSA is Swiss law and binds
as cited. MiFID II is a **Directive**, so what binds a firm is the national
transposition — and where a request names no member state, the EU side of the
comparison is a floor rather than the operative rule. The MiFID II SME records
its transposition position for exactly this reason; read it before treating the
two sides as like for like.

Neither SME resolves this. Each states its own segments on its own tests, and
`reg-comparison` classifies the pairing on the evidence. Expect
`PARTIAL_ALIGNMENT` and `NO_EXACT_EQUIVALENT` findings here more often than
`CONFIRMED_ALIGNMENT`, and treat a clean alignment claim as something to check
rather than to accept.

## Out-of-scope regimes

SFTR, CSDR, Dodd-Frank / CFTC Part 43-45, UK EMIR, UK MiFIR, ASIC/MAS/HKMA
reporting, AnaCredit, MMSR, Basel/CRR reporting, AMLA/GwG, and the Swiss
Banking Act are **not covered**. When a request touches them, the orchestrator
classifies it `UNSUPPORTED_DOMAIN`, says plainly which part it cannot cover, and
either proceeds on the covered part with the gap flagged or stops. It never
routes an out-of-scope question to the nearest-looking SME.
