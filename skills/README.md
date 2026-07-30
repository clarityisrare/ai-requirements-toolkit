# Requirements Engineering Skills

Downloadable [Claude skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills)
built from this toolkit. Where the top-level folders give you files to copy and
prompts to paste, these skills let Claude **run the workflows for you** — asking
the right questions, applying the method, shaping the output with the bundled
templates, and self-checking against the bundled checklists.

They follow the requirements lifecycle, in order:

| # | Skill | When it fires |
|---|---|---|
| 1 | [`elicitation-planner`](./elicitation-planner) | A thin business request arrives — frame it, map stakeholders, and plan the discovery or validation workshop |
| 2 | [`requirements-writer`](./requirements-writer) | Draft testable, traceable requirements, user stories, acceptance criteria, and NFRs (with feature patterns) |
| 3 | [`requirements-reviewer`](./requirements-reviewer) | Review/audit existing requirements for ambiguity, risk, completeness, and readiness |
| 4 | [`test-case-generator`](./test-case-generator) | Turn acceptance criteria into executable test cases + a traceability matrix |
| 5 | [`requirements-diagrams`](./requirements-diagrams) | Generate tailored Mermaid diagrams for a spec |

Each skill is self-contained: a `SKILL.md` plus a `references/` folder holding the
prompts, templates, checklists, patterns, and diagrams it needs.

## Installing

### As a plugin (recommended)

All five skills ship as one Claude Code plugin. Add this repo as a plugin
marketplace, then install the bundle:

```
/plugin marketplace add clarityisrare/ai-requirements-toolkit
/plugin install requirements-toolkit@ai-requirements-toolkit
```

Update later with `/plugin marketplace update ai-requirements-toolkit`.

### A single skill by hand

Prefer just one? Copy its folder into your Claude skills directory:

```bash
# Claude Code (personal skills)
cp -r elicitation-planner ~/.claude/skills/
```

Either way, once installed you just describe your task in plain language — e.g.
*"business asked us for a document upload feature, help me prepare for the
kickoff"* — and the matching skill triggers on its own.

## How they fit together

The skills hand off to each other along the lifecycle: elicitation feeds the
writer, the writer feeds the reviewer and the test generator, and diagrams support
any stage. A human — Requirements Engineer, Product Owner, or SME — always owns the
final decision.

---

> ⭐ **If any of this saves you time, please star the repo.** Each star tells me the
> toolkit is useful and worth expanding. It costs you a click and means a lot.
