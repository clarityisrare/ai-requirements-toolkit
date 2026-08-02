# Requirements Engineering Skills

Downloadable [Claude skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills)
built from this toolkit. Where the top-level folders give you files to copy and
prompts to paste, these skills let Claude **run the workflows for you** — asking
the right questions, applying the method, shaping the output with the bundled
templates, and self-checking against the bundled checklists.

They follow the requirements lifecycle, in order:

| # | Skill | When it fires |
|---|---|---|
| 1 | [`requirements-start`](./requirements-start) | A thin business request arrives — frame it, map stakeholders, and plan the discovery or validation workshop |
| 2 | [`requirements-writer`](./requirements-writer) | Draft testable, traceable requirements, user stories, acceptance criteria, and NFRs (with feature patterns) |
| 3 | [`requirements-reviewer`](./requirements-reviewer) | Review/audit existing requirements for ambiguity, risk, completeness, and readiness |
| 4 | [`requirements-test-cases`](./requirements-test-cases) | Turn acceptance criteria into executable test cases + a traceability matrix |
| 5 | [`requirements-diagrams`](./requirements-diagrams) | Generate tailored Mermaid diagrams for a spec |

Each skill is self-contained: a `SKILL.md` plus the `references/` and `assets/` it
needs — `references/` holds the methods, prompts, checklists, and patterns Claude
reads as it works, and `assets/` holds the templates and diagrams it fills in.

## Installing

### New to Claude Code? Start here 🌱

Never installed a Claude Code plugin before? Follow these four steps exactly — no
prior experience needed.

**1. Install Claude Code (one time).**
These skills run *inside* Claude Code, Anthropic's AI assistant for your terminal.
If you don't have it yet, follow the official guide:
[docs.claude.com/en/docs/claude-code](https://docs.claude.com/en/docs/claude-code).
Once it's set up, start it from any terminal by typing `claude` and pressing Enter.
The first time, it walks you through signing in. You'll then see a prompt like `>` —
that's where you type everything below.

**2. Add this toolkit as a "marketplace" (one time).**
A *marketplace* is just the place Claude Code downloads the skills from. At the `>`
prompt, type this and press Enter:

```
/plugin marketplace add clarityisrare/ai-requirements-toolkit
```

**3. Install the five skills.**
Now install the whole bundle:

```
/plugin install requirements-toolkit@ai-requirements-toolkit
```

Confirm if it asks. That's it — the skills are installed and ready.

**4. Use them — just describe your task in plain English.**
You don't run a command or pick a skill by name. Tell Claude what you're working on
and the right skill wakes up on its own. Try one of these at the `>` prompt:

- *"The business asked us for a document-upload feature — help me prepare for the kickoff workshop."* → starts you in `requirements-start`
- *"Draft testable requirements and acceptance criteria for password reset."* → `requirements-writer`
- *"Review this user story for ambiguity and missing cases."* → `requirements-reviewer`

**Keeping them up to date.** When the toolkit changes, pull the latest with:

```
/plugin marketplace update ai-requirements-toolkit
```

Already comfortable with Claude Code? The quick version is right below.

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
cp -r requirements-start ~/.claude/skills/
```

Either way, once installed you just describe your task in plain language — e.g.
*"business asked us for a document upload feature, help me prepare for the
kickoff"* — and the matching skill triggers on its own.

### In OpenAI Codex

Codex uses the **same `SKILL.md` format**, so this one bundle works there too — no
separate copy of the skills. The repo ships a Codex manifest
([`.codex-plugin/plugin.json`](../.codex-plugin/plugin.json)) alongside the Claude one,
both pointing at the same [`skills/`](.) folder.

Codex added a plugin marketplace in 2026 with the same command shape as Claude Code.
Before running the commands below, install the **GitHub plugin** — you can do this via
the plugin link found in the left menu. Then, at the Codex prompt, add this repo as a
source and install the bundle:

```
/plugin marketplace add clarityisrare/ai-requirements-toolkit
/plugin install requirements-toolkit
/reload-plugins
```

Then use it exactly like in Claude Code — describe your task in plain English and the
matching skill triggers on its own.

> ⚠️ The Codex marketplace is new. If `/plugin install` reports a different identifier
> after you add the source, use the one Codex shows. The commands above follow Codex's
> documented syntax — check the official Codex plugin docs before publishing, and note
> that listing in Codex's *curated* directory may not be self-serve yet (installing
> straight from this repo works regardless).

## How they fit together

The skills hand off to each other along the lifecycle: elicitation feeds the
writer, the writer feeds the reviewer and the test generator, and diagrams support
any stage. A human — Requirements Engineer, Product Owner, or SME — always owns the
final decision.

---

> ⭐ **If any of this saves you time, please star the repo.** Each star tells me the
> toolkit is useful and worth expanding. It costs you a click and means a lot.
