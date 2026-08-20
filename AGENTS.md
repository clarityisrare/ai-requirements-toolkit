# AGENTS.md

Guidance for AI coding agents (OpenAI Codex and any AGENTS.md-aware tool) working in this
repository. Claude Code reads `CLAUDE.md` for the same purpose.

## What this repo is

Two independent plugins published from one marketplace (`.claude-plugin/marketplace.json`
for Claude Code, `.agents/plugins/marketplace.json` for Codex). Both marketplace files
live at the repo root and point at the two toolkit folders.

1. **Requirements Engineering Toolkit** — `Toolkit_RE/`. Five guided *skills* for
   AI-assisted requirements work, plus standalone Markdown checklists, prompts, patterns,
   templates and diagrams. See [`Toolkit_RE/AGENTS.md`](./Toolkit_RE/AGENTS.md) for the
   guidance that applies inside it.
2. **Regulatory Reporting Intelligence Toolkit** — `Toolkit_RegRep/`. A multi-agent
   pipeline for Swiss and EU reporting regimes, with its own `skills/`, `agents/`,
   `reference/`, `templates/` and `checklists/`. See its `README.md`.

Each toolkit carries its own `.claude-plugin/plugin.json` and `.codex-plugin/plugin.json`.
The marketplace files at the root are the only place the two are listed together.

## Working here

- **Keep the toolkits independent.** They share this repository and nothing else. Don't
  introduce cross-references, shared files, or imports between them.
- **Don't move the toolkit folders.** `clarityisrare.com` deep-links into
  `Toolkit_RE/` and `Toolkit_RegRep/` subfolders by path, and both marketplace files
  publish the plugins by those paths. Renaming either folder breaks the website links and
  every install.
- **Register any new plugin in both marketplace files**, with a `source` path pointing at
  its folder.
- **Bump the version** in a toolkit's `plugin.json` *and* its entry in both marketplace
  files together, so an existing install re-materialises from the cache.
