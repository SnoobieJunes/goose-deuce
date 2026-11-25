# NEW-PROJECT-GUIDE.md — five steps from empty folder to running task loop

<!-- GUIDE — followed during setup; if copied into a new project folder alongside
     idea.md, remove this file and prompts-template.md before committing T-000.
     A human launches it with prompts-template.md → "Scaffold A — new-project
     kickoff"; the recurring step-5 session is launched with Scaffold D.
     Master: https://github.com/SnoobieJunes/goose-deuce (templates/NEW-PROJECT-GUIDE.md)
     Template version 1.2 (2026-11-21): genericized paths, added drop-in idea.md +
     clarifying-questions flow, starter TASKS-TEMPLATE.md, existing-repo T-000
     callout, Windows-safe CLAUDE.md / Goose notes, and accurate Hermes cap details.
     Template version 1.1 (2026-08-16). Changes to the master get a dated line here.

     The guide works because of four properties; keep them if you amend it:
       1. Every step ends with a runnable verification gate and a commit — a step
          whose output was never run is scaffolding theatre.
       2. Steps 1–3 are setup, step 4 is the perpetual task loop, step 5 is the
          recurring sweep. Scaffold-A sessions stop after step 3 for owner
          review — the backlog gets human eyes before any product code is written.
       3. The process files (AGENTS.md, TASKS.md, goose-deuce.md, docs/PLAN.md)
          exist and agree with each other BEFORE the first product code, so no
          work ever happens off the books.
       4. Single source of truth: this guide never restates a rule AGENTS.md or
          goose-deuce.md owns — it points. The one thing this guide owns is the
          step-5 audit checklist, which those files point back to.

     Prerequisites: git; the stack's toolchain (or authority to propose one); either
     `idea.md` (or `plan.md`) in the project folder OR a one-sentence product goal
     from the owner; the goose-deuce templates (dropped in or cloned at ⟨kit path⟩). -->

Follow the steps in order. Do not skip a gate; do not proceed past a red one.
Every commit follows AGENTS.md → Version control; commits made before the test
gate exists fall under AGENTS.md → Definition of Done → **Bootstrap exception**
(waived items named honestly in the body, e.g. `Tests: none yet — gate arrives
in T-002`).

> **Adopting an existing repo?** Do not run `mkdir` / `git init`. Copy
> `AGENTS-TEMPLATE.md` → `AGENTS.md`, `GOOSE-DEUCE-TEMPLATE.md` → `goose-deuce.md`,
> and `TASKS-TEMPLATE.md` → `TASKS.md`, create `docs/PLAN.md` and `CHANGELOG.md`,
> wire `CLAUDE.md`, fill `AGENTS.md`'s Snapshot from the real codebase, and replace
> `T-000`..`T-003` with **`T-000: establish the gate`** — run the existing suite
> as-is, file any currently red tests as `[!]` items, set the coverage floor to the
> **measured** baseline (never a wish), verify a cold clone passes, and enter step 4.

The bootstrap tasks, seeded in step 1:
**T-000** scaffold (closed in step 1) · **T-001** plan + backlog + living docs
(step 2) · **T-002** toolchain + test gate (step 3) · **T-003** walking skeleton
(the first step-4 loop task) · **T-004** the first standing goose-deuce sweep
(sits in `## Later` until the AGENTS.md → Deviations cadence hits).

## Step 1 — Scaffold the repo and wire the process

0. **If `idea.md` (or `plan.md`) is already in the project folder:** read it first,
   then ask the owner clarifying questions for anything ambiguous, missing, or
   underspecified (platforms, stack tradeoffs, scope limits, hard constraints) before
   locking `docs/PLAN.md` and `TASKS.md`. Keep `idea.md` in git (or fold it into
   `docs/PLAN.md` in step 2; if you used root `plan.md`, remove it after folding into
   `docs/PLAN.md` so case-insensitive filesystems never collide).

1. Create the project and repo (skip `mkdir` if you already copied the templates into
   your project folder):

   ```bash
   mkdir -p ~/⟨ProjectName⟩
   cd ~/⟨ProjectName⟩
   git init
   ```

2. Copy/rename the templates (from this folder or `⟨kit path⟩/templates/`) and
   instantiate them:
   - `AGENTS-TEMPLATE.md` → `AGENTS.md`
   - `GOOSE-DEUCE-TEMPLATE.md` → `goose-deuce.md`
   - `TASKS-TEMPLATE.md` → `TASKS.md`
   - `LOOP-TEMPLATE.md` → `LOOP.md` *(only if the repo will run autonomous
     `/loop` sessions; remove/skip otherwise. Its hook line is added to AGENTS.md.)*
   - `HERMES-OVERLAY-TEMPLATE.md` → `HERMES-OVERLAY.md` *(only if the repo will
     be worked in Hermes; remove/skip otherwise. Adds Hermes-native rules on top of
     AGENTS.md. Never name it `.hermes.md` or `HERMES.md` — Hermes loads context
     files first-match-wins and would suppress AGENTS.md altogether.)*
   - Remove kit-only files (`NEW-PROJECT-GUIDE.md`, `prompts-template.md`, and any
     uninstantiated `*-TEMPLATE.md` copies) before committing `T-000` so no
     template-of-templates enters a project repo.
   - Fill every `⟨…⟩` per the placeholder legend in AGENTS.md's TEMPLATE comment
     (format specimens in `<…>` stay). Items that need the toolchain (commands,
     coverage floor) are filled with the marker `⟨TBD step 3⟩`. Then delete each
     file's TEMPLATE comment block and goose-deuce.md's WORKED-EXAMPLE block.
   - Wire harnesses to the single source of truth: `ln -s AGENTS.md CLAUDE.md`
     (POSIX) or a one-line `CLAUDE.md` reading `@AGENTS.md` / "Read AGENTS.md before
     doing anything else." (Windows-safe). Codex, Cursor, OpenCode, and current Goose
     read `AGENTS.md` natively (older Goose: put that line in `.goosehints`).

3. Review `TASKS.md` (seeded with T-000…T-004 above from `TASKS-TEMPLATE.md` or
   AGENTS.md → The task board), checking each has `Why / Accept / Touches /
   Depends / Gated` — T-003's Accept is the smallest end-to-end slice that proves
   the architecture ⟨e.g. CLI prints version from a real module; app launches to
   an empty screen; library imports and one public call round-trips⟩. T-004
   (`goose-deuce sweep`) goes in `## Later` with `Gated: cadence`; task-loop
   step 9 promotes it when the cadence hits, and each sweep files its successor.

4. Create the layout so AGENTS.md's table is true from the first commit: the
   `src/`-equivalent and `tests/` directories (`.gitkeep`), `docs/PLAN.md` as a
   one-line stub ("Normative plan — written in T-001."), `CHANGELOG.md`
   containing only its contract comment, the stack's `.gitignore` (build
   outputs, caches, `.env`, secrets), and a two-line `README.md` stub: the
   one-sentence goal + "Process: see AGENTS.md."

**Gate (run it):**
`grep -rn "⟨" . --include="*.md" --exclude="CLAUDE.md" --exclude-dir=.git --exclude-dir=.venv --exclude-dir=node_modules | grep -v "TBD step 3"`
returns nothing; `grep -n "WORKED-EXAMPLE" goose-deuce.md` returns nothing;
every path in the Layout table (AGENTS.md → Project snapshot) exists;
`CLAUDE.md` resolves (`readlink CLAUDE.md` prints `AGENTS.md`, or `CLAUDE.md`
points to `AGENTS.md`).

**Commit:** `T-000: scaffold ⟨ProjectName⟩ from templates` — T-000 goes `[x]`
DONE `(date, this commit)` in this commit; the board is true from the first hash.

## Step 2 — Define the product and seed the plan  *(T-001)*

1. Write `docs/PLAN.md` — **the normative plan every goose-deuce.md `Plan:`
   field measures against.** It contains: the goal (incorporating `idea.md` and
   clarifications); the users and what success
   observably looks like; the architecture sketch (modules and seams, per
   AGENTS.md → Engineering standards); phases or milestones; explicit non-goals.
   Date it. The step-5 sweep is what amends it later.

2. Expand `README.md`: what this is, for whom, how it will be installed/run/
   tested — commands not yet real are written `arrives in T-002`, never implied.

3. Add CHANGELOG.md entries for T-000 and T-001 per its contract in AGENTS.md →
   Documentation protocol.

4. Decompose the plan's first phase into the TASKS.md backlog: each task with
   `Why / Accept / Touches / Depends / Gated`, in priority order, T-002 then
   T-003 first. **Accept lines name commands and observable results** (runnable
   the moment the toolchain lands); a task whose Accept an agent cannot execute
   is not pickable.

**Gate (run it):** every open task carries all five field lines — mechanically,
each of `grep -c "Why:" TASKS.md`, `"Accept:"`, `"Touches:"`, `"Depends:"`,
`"Gated:"` ≥ `grep -c '^- \[ \]' TASKS.md`. In the session report (judgement,
not gate): the plan's phase-1 items listed beside the board items, one-to-one.

**Commit:** `T-001: plan, backlog, and living docs` — T-001 closed in it.

## Step 3 — Toolchain and the test gate  *(T-002)*

1. Install and **pin** the toolchain: interpreter/compiler version pinned in a
   file the tooling reads (`.python-version`, `.nvmrc`, `rust-toolchain.toml`,
   …). One pinned version across every machine and CI — "works on my machine"
   claims are worthless when three machines can resolve three interpreters.

2. Configure the mechanical gates: formatter (check mode for the gate), linter,
   type-checker, zero-warning baseline (AGENTS.md → Engineering standards).

3. Stand up the test framework with one real smoke test exercising a genuine
   entry point (not `assert True`). This code carries the comment standard from
   its first line, stamped `[YYYY-MM-DD T-002]`.

4. Replace every `⟨TBD step 3⟩` marker across the repo —
   `grep -rn "TBD step 3" . --include="*.md"` finds them all (the snapshot
   commands, the coverage floor, LOOP.md's fast-test line, the DoD scan command,
   …) — with the real values, then **run each command and fix until all pass as
   written.** Set the coverage floor from the measured number, not a wish.

5. ⟨If the project has CI / multiple platforms:⟩ add the CI stub running the
   full gate on every platform named in the snapshot. ⟨Optional: a pre-commit
   hook running the fast gate.⟩

**Commit:** `T-002: toolchain and test gate` — T-002 closed in it. T-002's
Accept is the snapshot commands passing in the working repo; the cold clone
below is the *step's* gate, deliberately after the commit it needs. (The clone
sees only committed content; commit first is the correct order.)

**Gate (run it, after the commit):** placeholders all gone — `grep -rn "⟨" . --include="*.md" --exclude="CLAUDE.md" --exclude-dir=.git --exclude-dir=.venv --exclude-dir=node_modules`
returns nothing at all (no `TBD step 3` exemption) — and cold
checkout: `git clone . ⟨absolute scratch path, e.g. /tmp⟩/⟨ProjectName⟩-cold`,
then in the clone: setup command → full gate → green, exactly as the snapshot
writes them. If the clone fails the gate, file the fix at the **top** of
`## Now` (`T-005+` — it outranks T-003) and re-run; the step is not done until
the cold clone is green.

**→ Scaffold-A sessions stop here and report to the owner:** what was created;
every command run with its observed result (proven vs. inferred, labeled); the
seeded backlog for review. The task loop starts only after that report.

## Step 4 — Run the task loop  *(the perpetual state)*

Work now proceeds **only** through AGENTS.md → The task loop, one task at a time,
starting with T-003 (walking skeleton). The law is AGENTS.md in full — comment
standard, testing protocol, docs sweep, deviation trigger, push policy — pointed
at, not restated here.

Humans launch these sessions with prompts-template.md → Scaffold B (one task per
session is the default); reviews with Scaffold C; the recurring sweep with
Scaffold D; Hermes sessions with Scaffold E. Autonomous loops read LOOP.md first. This step has no exit — it ends
only when the project does; step 5 runs *inside* it, as board work, at the
cadence AGENTS.md → Deviations sets.

## Step 5 — Sweep, audit, upstream  *(the standing sweep task, at the AGENTS.md cadence)*

Run as its own session (Scaffold D). The sweep is a TASKS.md item; its commits
are ordinary commits. This checklist is the one thing this guide owns — AGENTS.md
→ Deviations and goose-deuce.md → Rules point here.

1. **goose-deuce sweep** — the three actions defined in goose-deuce.md → Rules →
   "The sweep": fold pending `Plan:` adjustments into docs/PLAN.md; verify every
   `[deferred]`/`[tech-debt]` entry has a live TASKS.md item (restore orphans,
   append the `[Correction, …]`); close with the `[process]` marker entry naming
   the range covered, and file the next sweep task.

2. **Docs audit:** run every command README.md and the AGENTS.md snapshot claim,
   as written; CHANGELOG.md has its entry for every task closed since the last
   sweep; board statuses match `git log`. Fix what lies, in this session's
   commits.

3. **Test audit:** run the coverage command against the snapshot floor — ratchet
   the floor up to just under the measured number when it has comfortably risen;
   zero flaky tests tolerated (each becomes a task); full-gate wall time still
   acceptable.

4. **Adversarial review:** a Scaffold-C session (findings-only) over everything
   since the last sweep — lenses: correctness, security, data loss, comment/doc
   honesty (comments asserting the unexercised are findings). **This sweep
   session files the returned findings as TASKS.md items in its own commit** —
   findings never evaporate and never become drive-by fixes.

5. **Upstream:** anything that cost an hour goes in the snapshot's foot-gun
   list. Improvements to the process files worth keeping across projects are
   **proposed to the owner as diffs** against the masters in the goose-deuce kit
   (https://github.com/SnoobieJunes/goose-deuce) — applied via PR / owner approval, dated in each master's header
   line. Masters ratchet the same
   direction the coverage floor does.

6. **Token audit:** re-measure AGENTS.md bytes (`wc -c AGENTS.md`) against your
   harness's context-file cap. Hermes scales `context_file_max_chars` dynamically
   at ~6% of the model's context window (20,000-char floor for small/unknown-window
   models; ~30.7k at 128k, ~48k at 200k, ~240k at 1M) and keeps 70% head + 20% tail
   while dropping the middle with a warning above the cap. If it exceeds your target
   cap, trim or move detail to `docs/` and reference it. Also flag any growth > 5%
   since the last sweep: justify or trim. Every character here is injected into
   every turn; the snapshot is the only section that grows with the project.

**Gate (run it):** the stranger test, literally — spawn a fresh sub-agent given
only AGENTS.md, TASKS.md, and the most recent goose-deuce.md entries (count per
AGENTS.md → Session ritual); it must name the next eligible task and quote its
Accept commands correctly. If it can't, what it tripped on is this sweep's last
finding — file it. That test passing is the whole point of the system.
