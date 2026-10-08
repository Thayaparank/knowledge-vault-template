<!-- TEMPLATE: project repo router — lightweight session router.
Copy into the project repo root in the FIRST commit, named for the file your AI tool reads:
AGENTS.md (cross-tool), CLAUDE.md (Claude Code), GEMINI.md (Gemini CLI), or
.github/copilot-instructions.md (GitHub Copilot). Use one file; make any others one-line pointers to it.
Fill every <angle-bracket> slot; DELETE any section that doesn't apply.
RULES OF THIS FILE: router only. General rules live in the vault's operating manual
(<vault>/AGENTS.md) — NEVER copy them here. The vault manual is only read if your tool is
told to read it: see the vault README → "Connect your project repos". Architecture and
decisions live in the vault — link, don't restate. This file may ADD project-specific rules
or SPECIALIZE vault rules; it may never cancel one. Target: under ~50 lines. -->

# <ProjectName> (<one-word repo type: product monorepo / API / tool>)

> Read this first, every session. This is a **lightweight router only** — it contains no
> architecture and no decisions. Those live in the vault (`<path-to-your-vault>`), the
> source of truth. Do not copy vault content into this repo.

## What this is
<2–4 lines: what the product/tool does, who it's for, current phase.>
- `<folder>/` — <stack piece>; setup: `<command>`

## Sources of truth — read before non-trivial work
- `<vault>/AGENTS.md` — general rules (the contract). Read it at session start unless your tool already loads it.
- `<vault>/wiki/projects/<project>.md` — project hub (architecture, links).
- `<vault>/wiki/projects/<project>-status.md` — current state + NEXT pointer. **Read first when resuming.**
- `<vault>/wiki/projects/<project>-decisions.md` — locked/open decisions.
- `<vault>/outputs/<project>/` — specs and plans.

## Project-specific rules (additions to the vault contract)
<Only rules that exist NOWHERE else and apply ONLY to this repo, e.g.:
- DB discipline variant (database-first releases / migration-first with committed down()).
- Branch model (e.g. one working branch; main = releases, promoted on the owner's word).
- Commit gate for this repo (default: commit only on the owner's explicit go).
- Dev-only affordances and their exact scope.>

## Commands
- Run dev: `<command>`
- Tests / gates: `<command>` (all gates green before any commit)
