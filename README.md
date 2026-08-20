# Clarity Is Rare — AI toolkits

Two independent, plain-Markdown toolkits for people doing precise work alongside AI.
Each installs as its own Claude Code or Codex plugin from this one repository, and each
works just as well copied by hand into your own docs.

| Toolkit | For | Folder |
|---|---|---|
| **Requirements Engineering** | Turning vague business requests into clear, testable, traceable requirements | [`Toolkit_RE/`](./Toolkit_RE) |
| **Regulatory Reporting Intelligence** | Comparing Swiss and EU reporting regimes without an AI inventing the answer | [`Toolkit_RegRep/`](./Toolkit_RegRep) |

Install either, or both — they share nothing but this repository.

## Requirements Engineering Toolkit

Five guided skills that run the requirements workflow for you: plan elicitation, draft
testable requirements, review them, generate test cases, and produce spec diagrams —
plus 40+ standalone checklists, prompts, patterns, templates and Mermaid diagrams.

```
/plugin marketplace add clarityisrare/ai-requirements-toolkit
/plugin install requirements-toolkit@ai-requirements-toolkit
```

→ [Full documentation](./Toolkit_RE/README.md)

## Regulatory Reporting Intelligence Toolkit

Six jurisdiction-isolated subject matter experts — FMIA Art. 39, FMIA Art. 104, EMIR,
MiFIR transaction reporting, MiFID II client classification and FinSA client
segmentation — each analysing its own regime and nothing else, feeding a comparison,
convergence, output-quality and executive reporting pipeline with pinpoint citations and
an auditable trail.

```
/plugin marketplace add clarityisrare/ai-requirements-toolkit
/plugin install reg-reporting-toolkit@ai-requirements-toolkit
```

→ [Full documentation](./Toolkit_RegRep/README.md)

> ⚠️ It covers those six Swiss and EU regimes and nothing else — **FinIA/FINIG,
> AMLA/GwG, SFTR, UK and US regimes are all out of scope**. It produces decision support
> for a qualified professional to check, not advice, and comes with no warranty of any
> kind. Read
> [Scope, limits and disclaimer](./Toolkit_RegRep/README.md#scope-limits-and-disclaimer)
> before relying on any output.

## Star this repo ⭐

If either toolkit is useful to you, a star genuinely helps. It's a signal that this is
worth maintaining and growing. Thank you.

## Contributing

Issues and pull requests are welcome — new patterns, better prompts, and clearer wording
especially. Keep files as plain Markdown or Mermaid so they stay easy to reuse.

## License

Released under the [MIT License](./LICENSE).
