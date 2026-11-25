# TASKS.md — ⟨Project Name⟩ work queue

<!-- TEMPLATE — copy to <repo>/TASKS.md, fill every ⟨…⟩ (T-000 closes in Step 1),
     delete this comment block.
     Master: https://github.com/SnoobieJunes/goose-deuce (templates/TASKS-TEMPLATE.md)
     Template version 1.0 (2026-11-21): starter board pre-seeded with bootstrap tasks
     T-000..T-004 matching NEW-PROJECT-GUIDE.md and AGENTS.md → The task board. -->

<!-- One queue. New DONE entries at the top of ## Done. Tasks without observable
     acceptance criteria are not pickable — sharpen them first. -->

## Now

- [ ] T-001 — Define product plan, backlog, and living docs
      Why: establish normative docs/PLAN.md and concrete Phase-1 tasks before writing code
      Accept: `docs/PLAN.md` dated with non-goals and architecture seams; every `[ ]` task in `TASKS.md` carries Why/Accept/Touches/Depends/Gated
      Touches: docs/PLAN.md, README.md, CHANGELOG.md, TASKS.md   Depends: T-000   Gated: none

- [ ] T-002 — Set up toolchain and the test gate
      Why: every product commit needs a real automated gate before implementation starts
      Accept: `⟨TBD step 3 — snapshot gate command⟩` passes in the repo and Step 1's placeholder grep returns nothing (followed post-commit by Step 3's cold-clone gate)
      Touches: ⟨toolchain config, CI, tests/smoke, AGENTS.md, TASKS.md⟩   Depends: T-001   Gated: none

- [ ] T-003 — Walking skeleton (smallest end-to-end slice)
      Why: prove the architecture compiles, runs, and passes tests end to end before scaling features
      Accept: `⟨TBD step 3 — e.g. app launches / CLI prints version / library round-trips one call⟩` exits 0 with test coverage
      Touches: ⟨src/, tests/⟩   Depends: T-002   Gated: none

## Later

- [ ] T-004 — Standing goose-deuce sweep
      Why: keep docs/PLAN.md, TASKS.md, and goose-deuce.md reconciled on cadence
      Accept: `templates/NEW-PROJECT-GUIDE.md` → Step 5 checklist (https://github.com/SnoobieJunes/goose-deuce) complete; stranger test passes; `[process]` entry logged
      Touches: docs/PLAN.md, TASKS.md, goose-deuce.md, AGENTS.md   Depends: T-003   Gated: cadence

## Blocked

## Dropped

## Done

- [x] T-000 — Scaffold ⟨Project Name⟩ from goose-deuce templates (⟨YYYY-MM-DD⟩, this commit)
