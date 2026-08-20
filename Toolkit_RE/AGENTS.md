# AGENTS.md

Guidance for AI coding agents (OpenAI Codex and any AGENTS.md-aware tool) working in the
**Requirements Engineering Toolkit**. See the repository root `AGENTS.md` for how this
toolkit sits alongside the other one.

## What this toolkit is

Five guided *skills* for AI-assisted requirements work, plus standalone Markdown
checklists, prompts, patterns, templates, and diagrams. It installs as a Codex plugin
(`.codex-plugin/plugin.json`) and as a Claude Code plugin (`.claude-plugin/`); both read
the same `skills/` folder.

## Using the skills

Each skill lives in `skills/<name>/` with a `SKILL.md` describing when it fires. When a
user's task matches, **trigger the skill and follow its method — don't hand-roll the
workflow**. They follow the requirements lifecycle in order and hand off to each other.

| Skill | Use it when the user wants to… |
|---|---|
| `requirements-start` | frame a thin or new business request — stakeholders, glossary, and a discovery or validation workshop |
| `requirements-writer` | draft testable, traceable requirements, INVEST user stories, acceptance criteria, or NFRs |
| `requirements-reviewer` | review or audit existing requirements for ambiguity, risk, completeness, or readiness |
| `requirements-test-cases` | turn acceptance criteria into test cases and a traceability matrix |
| `requirements-diagrams` | produce Mermaid diagrams (context, use-case, state, sequence, traceability) for a spec |

## Ground rules

- **A human always owns the final decision** — Requirements Engineer, Product Owner, or
  SME. The skills draft and check; they do not approve.
- **Ground every output in the input.** Do not invent business rules, roles, numbers, or
  sources. Label inferences as assumptions and list gaps as open questions.
- **Be concise.** No preamble, no restating the input; produce the least that fully
  covers the need.

## When editing this toolkit

- Keep files **plain Markdown or Mermaid** so they stay easy to copy and reuse.
- Make **surgical changes** — match the existing style, and don't refactor or "improve"
  content you weren't asked to touch.
- The standalone flat folders (`checklists/`, `prompts/`, `patterns/`, `templates/`,
  `diagrams/`) mirror the content inside `skills/`. If you change one side, update the
  other so they stay in sync — the `skills/` copy is the source of truth for content,
  while the flat folders use working relative links between siblings.
- **Don't move this folder or the folders inside it.** `clarityisrare.com` deep-links
  `Toolkit_RE/skills/`, `patterns/`, `prompts/`, `checklists/`, `templates/`, `diagrams/`
  and `examples/` by path, and the plugin is published from the repository root
  marketplace files as `source: "./Toolkit_RE"`.
