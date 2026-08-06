# AGENTS.md — Vault Operating Manual

> Operating manual for an AI assistant (or a human) working inside this vault.
> Read this file first, every session, before touching any other file.
>
> This is the **single authoritative manual** for every AI tool. `CLAUDE.md` (Claude Code),
> `GEMINI.md` (Gemini CLI), and `.github/copilot-instructions.md` (GitHub Copilot) are
> one-line pointers to this file — edit the rules here, never in the pointers.

---

## 1. Purpose of the Vault

This vault is a **long-term personal memory** — a structured, AI-optimized knowledge base for the owner's work. It exists to:

- Capture solved problems, decisions, and procedures so they are never re-solved from scratch.
- Provide a curated, indexed knowledge surface that an assistant can retrieve from at minimal cost.
- Convert raw notes, documents, and conversations into distilled, searchable lessons.

Every file should still be useful 12 months from now.

---

## 2. Folder Responsibilities

| Folder | Purpose | Mutability |
|---|---|---|
| `raw/` | Immutable inbox. Original documents, notes, conversations — the audit trail. | **Read-only** for the assistant. The owner adds files; nobody edits history. |
| `wiki/` | Curated, distilled knowledge. One concept per page. The retrieval layer. | **Editable** — improved over time |
| `wiki/projects/` | Per-project hub + status + decisions + changelog files. | Editable |
| `outputs/` | Generated deliverables — reports, exports, drafts. | Editable, disposable |
| `templates/` | Canonical templates for each note type. Copy, don't edit in place. | Editable (rare) |
| `daily_notes/` | Daily journal entries (`YYYY-MM-DD.md`). | Append-only |

---

## 3. Core Rules

These rules apply in every session.

1. **`raw/` is immutable.** Never edit, rename, reformat, or delete a file in `raw/`. Treat it as evidence. Reading is fine; that's what it's for.
2. **One concept per wiki page.** If a page covers two problems, split it. Pages should be small enough to retrieve cheaply (target: under 200 lines).
3. **Wiki pages are derivative.** Every wiki page cites at least one `raw/` source by relative path.
4. **Prefer linking over duplicating.** One fact lives in exactly one authoritative file; everywhere else links to it.
5. **kebab-case filenames.** Lowercase, hyphen-separated, `.md`. Raw files carry a `YYYY-MM-DD-` prefix; wiki pages are timeless and carry no date.
6. **Concise, structured markdown.** Front-matter, headings, bullets. No prose walls.
7. **Cross-link aggressively.** Every wiki page ends with a `## Related` section (2–5 links) and a `## Sources` section (raw links).
8. **Update the index.** Every new wiki page gets a line in `wiki/index.md`.
9. **Log every change.** One line in `log.md` per ingestion or update: `YYYY-MM-DD | actor | action | files touched` — max ~200 characters. Details live in the pages, never in the log.
10. **No noise.** If a note doesn't teach something reusable, it belongs in `raw/` or `daily_notes/`, not `wiki/`.
11. **No secrets in the vault.** Passwords, keys, tokens, and account numbers live outside; reference them as `<SECRET: name>` placeholders. If a live secret is found in a file, flag it for removal immediately.
12. **Checkpoint before stopping.** Never end a session with unsaved state — update the project status file (with an exact resume pointer), record decisions, append changelog and log lines. A brand-new session reading the status page must be able to continue with zero questions.
13. **Token efficiency.** Follow [token-efficiency.md](token-efficiency.md) in every session: reference paths instead of pasting, one task per conversation, search narrow (never whole-vault scans), grep the log. If the owner does something token-wasteful, point out the cheaper alternative once — then do the work anyway.

**Developers:** an optional add-on with engineering rules for AI-assisted coding (layered architecture, approval gates, delegation supervision, git discipline, QA walks) lives in [engineering-rules.md](engineering-rules.md) — adopt it or delete it.

---

## 4. Workflow: Ingesting New Knowledge

When new material lands in `raw/`:

1. **Read the raw source.** Do not modify it.
2. **Classify it** into one of the wiki categories.
3. **Check the wiki first.** If a page on the concept exists → extend it; never create a duplicate. If none exists → create one from the matching file in `templates/`.
4. **Distill, don't copy.** Extract the reusable lesson — cause, resolution, principle. Strip incidental detail.
5. **Cite the raw source** at the bottom of the page.
6. **Cross-link** to related pages (or note that none exist yet).
7. **Update `wiki/index.md`** and **append a line to `log.md`**.

---

## 5. Workflow: Updating Wiki Pages

1. **Read the existing page first.**
2. **Edit in place** — never fork a duplicate.
3. Append a dated entry to a `## Revision history` section at the bottom.
4. **Preserve cross-links.** If a page is renamed, find inbound links and update them; leave a redirect note at the old path.
5. **Log the update** in `log.md`.

---

## 6. Project Continuation

When resuming a project, read these first if they exist — they are the authoritative continuation source:

- `wiki/projects/<project>-status.md` — current state and the `NEXT ← RESUME HERE` pointer.
- `wiki/projects/<project>-decisions.md` — a recorded decision is settled; don't re-argue it, but do check its premise is still true.
- `wiki/projects/<project>-changelog.md` — append-only history; one dated line per session that changes the project.

The hub (`wiki/projects/<project>.md`) holds the stable reference: background, key facts, links. Volatile state never goes in the hub.

---

## 7. Rules Hierarchy — this vault and your project repos

Rules live at levels; a lower level may **add to or specialize** a higher one — never cancel it.

1. **This manual (AGENTS.md)** — the one home for every general rule. It applies in every
   session, in every repo. General rules are never copied anywhere else.
2. **Assistant memory** (if your tool has one) — only learnings *not yet* promoted into this
   manual. When a learning becomes a rule here, delete the memory copy — a rule stated in two
   always-loaded places will eventually say two different things.
3. **Each project repo's own `CLAUDE.md`/`AGENTS.md`** — a lightweight **router**: what the
   repo is, stack, commands, pointers back to this vault, plus rules that exist ONLY for that
   project. Start it from [templates/project-claude-md-template.md](templates/project-claude-md-template.md)
   in the repo's first commit. It never restates general rules and never holds status.
4. **Continuation files** (`-status` / `-decisions` / `-changelog`) — volatile per-project state.

Two habits keep this conflict-free: **date every rule** (newest dated statement wins), and
**treat a found conflict as a bug** — fix it at its source the moment it's spotted.

---

## 8. Optimization for Retrieval

- Lead every wiki page with a one-line `summary:` in the front-matter and a `tags:` list.
- Use consistent headings: `## Situation`, `## Root cause`, `## Resolution`, `## Why it works`, `## Related`, `## Sources`.
- Never embed huge dumps in wiki pages — link to `raw/` instead.
- Search `wiki/` before `raw/`; return the wiki link, not a full restatement.
- Full cost-saving practices: [token-efficiency.md](token-efficiency.md) — follow it in every session.

---

## 9. Make It Yours

This manual is a starting point. When something goes wrong in your workflow, add the prevention here as a new numbered rule — dated, with one line on why. That habit is what turns a folder of notes into a system that improves itself.

---

*This file is the contract. When in doubt, re-read it.*
