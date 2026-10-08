---
title: QA Scenario — <feature name>
type: qa-scenario
project: <project>
spec: <relative link to the spec this verifies>
date: YYYY-MM-DD
status: draft | ready-to-run | executed | blocked
tags: [<project>, qa, ui, <feature-slug>]
summary: One line — what a person walks through on screen, and what it proves.
---

# QA Scenario — <feature name>

> Canonical rule: [engineering-rules.md](../engineering-rules.md) §6 — every feature ships
> with a UI-based QA scenario, **written with the spec, before the build**. This document
> IS the acceptance definition for <feature>. The automated suite proves the API behaves;
> this proves the product works.

## 1. What this proves

Two or three lines in plain business language: what a real user can now do, and what would
be broken if these steps failed. Name what is explicitly **out of scope** (owned by unit
tests, another scenario, or a CI gate).

## 2. Preconditions

| Item | State / action |
|---|---|
| Servers / app | How the app is started for this run, and on which URL/port. |
| Database | Which environment, which seed/demo rows must exist. |
| Login | Which persona(s). **Note if the owner must type credentials live** — that makes the run user-gated. |
| Feature config | Settings/flags/keys the feature needs, and their values for this run. |
| Browser | Browser and viewport used. |
| Baseline | Test suite green at `<N passed>`; working tree clean at `<sha>`. |

## 3. Test data

What this run will CREATE (use markers like `qa.*@example.com` so it is findable), and the
exact cleanup step. A scenario that leaves unexplained rows in a shared database is not
finished.

## 4. Walkthrough

One row per user action. `Expected` is what appears **on screen** — a value, a state, a
message — never an HTTP code.

| # | Persona | Action (what you click / type) | Expected on screen | Result |
|---|---|---|---|---|
| 1 | <persona> | Navigate to `<url>` | <what renders> | ☐ |
| 2 | <persona> | <click/type> | <exact visible outcome> | ☐ |
| 3 | | | | ☐ |

## 5. Failure & validation paths

The unhappy paths a user can actually hit. Each one names the **message the user sees** —
a silent failure or a raw stack trace is itself a defect.

| # | Provoke it by | Expected user-visible behavior | Result |
|---|---|---|---|
| F1 | <invalid input / missing config / conflict> | <message, field highlight, blocked action> | ☐ |
| F2 | | | ☐ |

## 6. Permission variants

Only for gated features. Which role sees it, which gets a clean refusal (never a crash,
never a blank screen).

| # | Persona / permission | Expected | Result |
|---|---|---|---|
| P1 | holder of `<permission>` | feature visible and usable | ☐ |
| P2 | user without it | entry point absent; direct URL → clean refusal | ☐ |

## 7. Theme & responsive matrix

Mandatory for any visual change in a screen-based UI. Adjust the themes and widths to the
ones your product supports; delete this section if the feature has no screen.

| Surface | Light | Dark | 375 | 768 | 1280 |
|---|---|---|---|---|---|
| <screen> | ☐ | ☐ | ☐ | ☐ | ☐ |

Check for: unreadable contrast, hardcoded colors surviving the theme switch, horizontal
overflow at 375, controls falling off-canvas.

## 8. Console & network

- Browser console: **zero errors** (warnings noted).
- Network tab: no 404/500 on the screens walked — dead endpoints ship unnoticed unless
  someone looks.

## 9. Result

| Field | Value |
|---|---|
| Executed | YYYY-MM-DD / **not yet — blocked on <what>** |
| Outcome | PASS / FAIL / PARTIAL |
| Steps blocked | <ids + why: login, keys, environment> |
| Defects found | <ids + one line each> |
| Cleanup done | ☐ |

## 10. Defects found

Each defect: symptom → root cause → fix. Copy into the project's testing-history document —
the cause matters more than the fix; "fixed" alone teaches nothing.

| # | Symptom | Root cause | Fix |
|---|---|---|---|
| D1 | | | |

## Sources

- Spec: `<link to the spec this verifies>`
- Status: `wiki/projects/<project>-status.md`
- Testing history: `<project's testing-history document>`
