# Engineering Rules — Optional Add-on for Developers

> Rules for AI-assisted **software development**, distilled from real incidents in a
> working developer's vault. If your vault isn't about code, delete this file.
> Adopt what fits; every rule here earned its place by something going wrong without it.

---

## 1. Build like a senior architect — never a throwaway script

For any implementation task, engineer it the way an experienced senior architect would:

- **Layered separation of concerns.** Presentation, business logic, and data access each
  in their own place — no business rules in controllers, no SQL in the UI layer. Follow
  the existing project's architecture; don't invent a parallel structure.
- **Centralized error handling.** Services throw typed errors; exactly one boundary maps
  them outward. Nothing swallowed silently; internals never leak to clients.
- **Logging as its own cross-cutting layer.** An injected logger, not print statements
  scattered through methods. Log at boundaries and on failures — and never log secrets.
- **Requirement first.** Be clear on what the business needs and the edge cases before
  coding; state assumptions; keep each change small and easy to review.

If a shortcut is genuinely warranted (a spike, a throwaway), say so explicitly and get
agreement first.

## 2. Only approved work auto-runs

"Continue the project" authorizes continuing the **approved plan** — not inventing
decisions, widening scope, or spawning parallel work. The assistant asks first for:

- anything beyond the written spec, including "while I was in there" fixes;
- changing behavior that currently works — **especially anything touching money**;
- new features, refactors, dependencies, or schema changes not already approved;
- building on its own defaults that the owner never ratified.

And it **notifies every change**: what, why, and whether it is live or dormant (a change
behind a default-off flag is dormant — say so explicitly).

## 3. Supervise every delegated task — never fire-and-forget

When work is delegated (to a subagent, a cheaper model, or any automation):

- **Reduce first.** One small, self-contained task per delegation, with a written spec
  and acceptance checks. Too big to review in one pass = too big to delegate.
- **Set an expectation before launch** (time/steps) and check progress against it —
  don't wait blindly.
- **Diagnose failures, don't just retry.** Find why it failed (spec too big, missing
  context, wrong tier), fix that, then re-delegate.
- **Review 100% of results** and run the acceptance checks yourself before anything is
  committed. Repeated same-class findings mean the tasks are sized wrong.

## 4. Git discipline

- **One attribution policy, applied everywhere.** Teams differ: some require disclosing
  AI assistance (a trailer or a PR note), others want the owner's identity only. Follow
  your organisation's or project's policy; if there is none, pick one, write it here, and
  apply it to commits, PRs, code comments, and docs alike. Commit messages describe the
  change.
- **Commit on the owner's go**, per task (or a per-repo gate the owner defines, e.g.
  auto-commit when all test gates pass on approved-plan work).
- **Failing or unverified work is never committed.** Tests green first, changelog entry
  committed together with the change.
- **At every stop, work already approved to commit is committed AND pushed** to the
  working branch — a commit sitting only on one machine is not saved. This never creates
  commit permission: unapproved work stays on disk and is reported as uncommitted. Never
  push protected branches without the owner's word.
- **Never force-push** (`--force`, `--force-with-lease`) without the owner's explicit word,
  every time. An ordinary push is repairable with a follow-up commit; a force-push can
  delete the only remaining copy of someone else's work.
- **Commit named paths, never `git add -A`**, whenever more than one session or person
  works in the same folder — otherwise their half-finished files ride into your commit
  unreviewed.

## 5. No tracking code, ever

AI-generated code contains zero telemetry, analytics, tracking pixels, phone-home calls,
or obfuscated logic. If existing code or a new dependency ships any, call it out
explicitly before proceeding.

## 6. A green test suite is not proof the product works

For products with a user interface. Tests prove the API behaves; the proof a feature
works is walking the actual screens.
Write a UI-based acceptance scenario **with the spec, before the build** — steps a person
clicks, with the exact expected on-screen result per step. A feature shipped without its
walk isn't done. Defects found by a walk get a recorded root cause, never just "fixed".

A blank scenario ready to copy:
[templates/qa-test-scenario-template.md](templates/qa-test-scenario-template.md) — one row
per click, failure paths, permission variants, a theme/responsive matrix, and a per-step
pass/fail record.

## 7. Database changes are releases, not edits

Every schema change ships as a committed, ordered, immutable migration/release script
with a working rollback — never an auto-sync against a shared or production database.
Keep a schema snapshot and a one-entry-per-release changelog beside the scripts.

## 8. A failing check gets one re-run — then it is a defect

When lint, typecheck, tests, or a build goes red: one clean re-run, then the verdict.
Red twice **is** a defect — there is no third run. Green on the re-run is **reported**,
with the failing run's output, never counted as a clean pass: a flaky check is its own
item to fix. Judge every check by the **tool's own exit code**, never a pipeline's —
`npm run build | tail` returns `tail`'s exit code and reports success on a failed build.

## 9. Every bug fix ships a regression test

A test that reproduces that specific bug — failing before the fix, passing after. Beyond
that, unit tests earn their place on logic with branches (a calculation, a validation, a
state transition), not on plumbing.

---

## Related

- [AGENTS.md](AGENTS.md) — the vault's general operating manual (§7 rules hierarchy)
- [templates/project-router-template.md](templates/project-router-template.md) — per-repo router file
- [templates/qa-test-scenario-template.md](templates/qa-test-scenario-template.md) — acceptance-scenario blank for rule 6
- [token-efficiency.md](token-efficiency.md) — cost practices
