# Requirement Taxonomy

Every requirement an SME identifies carries exactly one **core type** and,
optionally, one **domain qualifier**.

Why the split: the originating Copilot agents each used their own list — 16
values for FMIA and EMIR, 22 for MiFIR, 26 for MiFID II. The comparison layer was
then asked to align findings across vocabularies that did not overlap, which
silently degrades every cross-jurisdiction comparison. One shared core vocabulary
makes findings comparable; domain qualifiers keep the precision that the longer
lists were carrying.

## Core types (shared by all SMEs — always assign exactly one)

| Type | Covers |
|---|---|
| `REPORTING_SCOPE` | What activity, product, or entity falls in or out of scope |
| `REPORTING_PARTY` | Who carries the obligation, including cascades and delegation |
| `REPORTING_TIMELINE` | Deadlines, cut-offs, T+n, lifecycle timing |
| `REPORTABLE_EVENT` | Which events trigger a report (new, modify, terminate, valuation, correction) |
| `REPORTABLE_INSTRUMENT` | Which instruments and underlyings are in scope |
| `REPORTABLE_DATA` | Fields, formats, content of the report itself |
| `IDENTIFICATION` | Identifiers and the rules for choosing them (LEI, UTI, UPI, ISIN, national identifiers, beneficial owner, decision makers, algorithms) |
| `DATA_QUALITY` | Accuracy, completeness, validation, error correction, remediation |
| `RECONCILIATION` | Inter-party or inter-repository reconciliation and matching |
| `VALUATION` | Mark-to-market / mark-to-model reporting |
| `COLLATERAL` | Margin and collateral reporting |
| `TRADE_REPOSITORY` | Interaction with a TR, ARM, APA, or reporting office |
| `TRANSPARENCY` | Pre- and post-trade transparency obligations |
| `CLEARING` | Clearing obligation and exemptions |
| `RISK_MITIGATION` | Non-cleared risk mitigation techniques |
| `CLIENT_ELIGIBILITY` | Client classification, categorisation, and the services each category may receive |
| `CONDUCT` | Suitability, appropriateness, product governance, disclosure, inducements, best execution, conflicts |
| `RECORDKEEPING` | Retention, reconstruction, audit evidence |
| `GOVERNANCE` | Ownership, oversight, board and committee responsibilities |
| `CONTROL` | Operating controls, monitoring, pre-trade blocking, exception handling |
| `OTHER` | Only when nothing above fits — and say why in the finding |

## Domain qualifiers (optional, one per requirement)

Use to preserve the precision of the original longer lists. Format:
`CORE_TYPE / QUALIFIER`.

**MiFIR transaction reporting:** `BUYER_SELLER_IDENTIFICATION`,
`NATIONAL_IDENTIFIER`, `LEI_REQUIREMENT`, `INVESTMENT_DECISION_MAKER`,
`EXECUTION_DECISION_MAKER`, `ALGORITHM_IDENTIFICATION`,
`FINANCIAL_INSTRUMENT_REFERENCE_DATA`, `ERROR_CORRECTION`

**MiFID II client classification:** `RETAIL_CLIENT`, `PROFESSIONAL_CLIENT`,
`ELECTIVE_PROFESSIONAL`, `ELIGIBLE_COUNTERPARTY`, `CLIENT_REPAPERING`,
`INVESTMENT_ADVICE`, `PORTFOLIO_MANAGEMENT`, `EXECUTION_ONLY`, `SUITABILITY`,
`APPROPRIATENESS`, `PRODUCT_GOVERNANCE`, `TARGET_MARKET`,
`DISTRIBUTION_STRATEGY`, `BEST_EXECUTION`, `DISCLOSURE`, `COSTS_AND_CHARGES`,
`INDUCEMENTS`, `CONFLICTS_OF_INTEREST`, `CLIENT_AGREEMENT`

**FMIA Art. 39:** `GOOD_TO_TRADE`, `TRADE_BLOCKING`, `PRE_TRADE_CONTROL`,
`REPORTING_OFFICE`, `BENEFICIAL_OWNER`

**EMIR / FMIA Art. 104:** `DELEGATED_REPORTING`, `LIFECYCLE_EVENT`,
`UTI_GENERATION`, `INTRAGROUP_EXEMPTION`, `REPORTING_CASCADE`

Examples:

```
IDENTIFICATION / LEI_REQUIREMENT
REPORTING_PARTY / REPORTING_CASCADE
CONDUCT / SUITABILITY
```

## Rule for comparison

`reg-comparison` aligns findings on the **core type first**. Two findings with
different core types are not comparable as a pair — if they seem related, that is
a `NO_EXACT_EQUIVALENT` or a structural difference worth stating, not an
alignment. Qualifiers add nuance to a comparison; they never create one.
