# Knowledge Vault Template

> A lean, copyable system for keeping what you learn permanently — and resuming any project with zero questions. Works for any field, with or without an AI assistant.

---

## The Core Idea

Keep one version-controlled folder of markdown files as your permanent memory. **Raw evidence goes in untouched; distilled lessons live in a small curated wiki.** Future questions get answered from short wiki pages — never by re-reading raw dumps.

This works for software engineering, research, law, writing, business operations — anything where you solve problems you don't want to solve twice.

---

## The Structure

```
vault/
├── raw/                  # Evidence — captured exactly as it happened, never edited
│   ├── documents/        # Source material: reports, articles, files as received
│   ├── conversations/    # Meeting notes, chat exports, AI conversations worth keeping
│   └── projects/         # One subfolder per project: scope docs, handovers
│
├── wiki/                 # Lessons — one concept per short page, improved over time
│   ├── index.md          # Master index — the entry point for every search
│   ├── lessons/          # Problem → cause → solution entries
│   ├── methods/          # Reusable procedures, checklists, recipes
│   ├── troubleshooting/  # Symptom → likely cause → check → fix flows
│   └── projects/         # One hub + continuation files per project
│
├── outputs/              # Deliverables you produce: reports, exports, drafts
├── templates/            # Blank note templates — copy, don't edit in place
├── daily_notes/          # Optional daily journal (YYYY-MM-DD.md)
├── AGENTS.md             # Operating manual for an AI assistant (optional but powerful)
└── log.md                # One line per change: date | actor | action | files
```

**Why two layers?** `raw/` is the audit trail — when a lesson is ever questioned, the original evidence settles it. `wiki/` is the retrieval layer — short pages are cheap for you (and an AI) to search and load. Dumping into `raw/` has zero formatting pressure; distilling happens when you have five minutes.

### Adapt the categories to your field

The folder names above are a neutral starting set. Rename the subfolders to match your work — the two-layer rule is what matters, not the labels.

| Field | `raw/` subfolders might be | `wiki/` subfolders might be |
|---|---|---|
| Software engineering | `bugs/`, `logs/`, `deployment/` | `bugs/`, `patterns/`, `sql/` |
| Research / study | `papers/`, `lecture-notes/`, `experiments/` | `concepts/`, `methods/`, `open-questions/` |
| Legal / business | `contracts/`, `meetings/`, `correspondence/` | `clauses/`, `playbooks/`, `precedents/` |
| Writing / content | `drafts/`, `references/`, `feedback/` | `techniques/`, `style-rules/`, `audience-notes/` |

---

## The Rules

1. **`raw/` is immutable.** Add files date-prefixed (`2026-08-04-payment-dispute-call.md`), never edit or rename them afterwards.
2. **One concept per wiki page**, under ~200 lines, with predictable headings: `Situation → Root cause → Resolution → Why it works → Related → Sources`.
3. **Every wiki page cites its raw source** and links 2–5 related pages. Link, never duplicate — one fact lives in exactly one file.
4. **kebab-case filenames** everywhere. Wiki pages are timeless (no dates); raw files are chronological (dated).
5. **Log every change** as one line in `log.md`; add every new page to `wiki/index.md`.
6. **No secrets in the vault.** Passwords, keys, account numbers live elsewhere; reference them as `<SECRET: name>` placeholders.

---

## The Learning Loop

Every time you solve something:

1. **Capture** — drop the evidence into `raw/` (the document, the conversation, the failed attempt).
2. **Distill** — write or extend one wiki page: the cause and the resolution, stripped of incidental detail.
3. **Connect** — cite the raw source at the bottom, cross-link related pages, update the index, add a log line.

### Worked example

You spend an afternoon on a recurring problem — say a vendor invoice that keeps getting rejected. You paste the rejection emails into `raw/documents/2026-08-04-invoice-rejection-thread.md`. Then you write `wiki/lessons/invoice-rejected-missing-po-reference.md`:

```markdown
---
summary: Invoices bounce when the PO number is only in the attachment — put it in the subject line
tags: [invoicing, vendor, process]
---
## Situation
Vendor invoices repeatedly rejected by the client's accounts system.

## Root cause
Their automated intake only reads the email subject; the PO number
was only inside the attached PDF.

## Resolution
Standard subject format: "Invoice <number> — PO <number>".

## Why it works
The intake system matches on subject text before a human ever sees it.

## Related
- [vendor-onboarding-checklist](../methods/vendor-onboarding-checklist.md)

## Sources
- [rejection thread](../../raw/documents/2026-08-04-invoice-rejection-thread.md)
```

Six months later the same symptom appears with a different client. One search — solved in two minutes instead of an afternoon.

---

## Per-Project Usage

Each active project gets **four small files** in `wiki/projects/`:

| File | Holds | Changes |
|---|---|---|
| `<project>.md` | The hub: background, key facts, links to raw sources and related pages | Rarely |
| `<project>-status.md` | Current state only, topped by a **`NEXT ← RESUME HERE`** pointer | Every session |
| `<project>-decisions.md` | Numbered decisions: locked, open, rejected — each dated with its reason | When a decision is made |
| `<project>-changelog.md` | Append-only dated history of what was done | Every session that changes the project |

Each file has one job, and they link to each other instead of repeating content.

### How a work session flows

1. **Open `-status.md` first.** The NEXT pointer tells you exactly where to continue — no re-reading old threads, no "where was I?".
2. **Check `-decisions.md`** before revisiting any choice. A recorded decision is settled; you never re-argue it from scratch.
3. **Do the work.**
4. **Before stopping:** rewrite the status (new NEXT pointer, anything half-done), record any decision made, append one changelog line.

The test of a good status file: **a person who has never seen the project reads it and can continue the work with zero questions.** If that isn't true, update it before you stop. This is what makes interruptions cheap — a project paused for three weeks resumes in minutes, whether it's you returning or an AI assistant picking it up fresh.

---

## Using It with an AI Assistant

The vault is designed so an AI assistant can work inside it safely:

- **[AGENTS.md](AGENTS.md)** is the operating manual the assistant reads first, every session. It encodes the rules above so the system maintains itself.
- It works with **any AI tool**: `AGENTS.md` is the cross-tool standard (Codex, Cursor, Windsurf, …), and `CLAUDE.md` (Claude Code), `GEMINI.md` (Gemini CLI), and `.github/copilot-instructions.md` (GitHub Copilot) are one-line pointers to it — one manual, every assistant.
- The assistant answers questions from `wiki/` pages (cheap, short) instead of re-reading raw files (expensive, long).
- The per-project status/decisions/changelog files let an assistant resume your project cold, with zero questions.

No AI? Everything still works — the manual is just as useful as a human checklist.

---

## Getting Started

1. Use this template (or clone it) and rename the category folders to fit your field.
2. Solve one problem and run the learning loop once: capture → distill → connect.
3. Add your own rules to [AGENTS.md](AGENTS.md) as you learn — when something goes wrong in your workflow, capture the prevention as a numbered rule. The vault improves itself this way.

Everything compounds from there.

---

## Contributing

Improvements to the structure, rules, and templates are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md). This repo is the **method only**; it ships empty of any real knowledge, and contributions should stay that way.
