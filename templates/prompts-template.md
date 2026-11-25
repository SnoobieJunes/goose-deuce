# prompts-template.md — scaffolds for launching agent sessions

<!-- TEMPLATE — lives in the goose-deuce kit (if copied into a new project folder
     for kickoff, remove it before committing T-000; the step-1 adoption gate greps
     for stray ⟨…⟩ and this file is full of them by design). To use: copy ONE
     scaffold out, fill every ⟨…⟩ — the variable part is always inside the brackets,
     one option survives a ⟨A | B⟩ — cut what doesn't apply, and paste it as the
     session's opening prompt.
     Master: https://github.com/SnoobieJunes/goose-deuce (templates/prompts-template.md)
     Template version 1.2 (2026-11-21): genericized paths to ~/⟨ProjectName⟩,
     removed private project/model-routing refs, added Variant A1 (drop-in idea.md +
     clarifying questions), fixed hermes --resume flag and trailing backtick typo.
     Template version 1.1 (2026-08-16). Changes to the master get a dated line here.

     Why these scaffolds are shaped this way: see "Anatomy" and "Anti-patterns"
     below — the operative rules live there, once.

     Wire it up: scaffold A pairs with NEW-PROJECT-GUIDE.md in this folder;
     B, C, and D assume the repo carries AGENTS.md, TASKS.md, and goose-deuce.md
     from these templates. -->

## Anatomy of a session prompt

Name these, in roughly this order — each maps to a line in the scaffolds:

1. **Location** — project path: `~/⟨ProjectName⟩` (or `.` inside the folder).
2. **Session start** — "run AGENTS.md → Session ritual (Start) in full" — point at
   the ritual; never restate a shortened version (a lossy copy wins by recency,
   then drifts).
3. **Task** — the goal in one sentence, then `T-###` by name or "pick the next
   eligible per AGENTS.md → The task loop → PICK".
4. **Session budget** — how many tasks; which models; how many subagents
   (e.g. "spawn at most ⟨2⟩ ⟨haiku/sonnet⟩ subagents; no forks of your own
   context").
5. **Verification** — the exact commands that must pass before any commit.
6. **Approval boundaries** — commit locally; never push without explicit approval;
   ask before anything destructive or outward-facing.
7. **Stop conditions** — budget spent, blocked on an owner decision, or nothing
   eligible to pick → record state per AGENTS.md and end cleanly. Never force
   progress, never invent work.
8. **Report format** — proven vs. inferred, labeled; deviations cited by date +
   title; board status for every task touched; lead with the fact, no sycophancy.

---

## Scaffold A — new-project kickoff

### Variant A1 — templates + `idea.md` (or `plan.md`) dropped into your folder

    Work in ~/⟨ProjectName⟩ (or `.` if launched inside the folder).

    I placed the goose-deuce templates and `idea.md` (or `plan.md`) here. Read
    `idea.md` and `NEW-PROJECT-GUIDE.md` first.

    Before scaffolding or locking in `docs/PLAN.md`, ask me any clarifying questions
    I have not answered (platforms, stack tradeoffs, scope limits, hard constraints).

    Once answered, follow steps 1–3 of `NEW-PROJECT-GUIDE.md` (removing kit-only
    `NEW-PROJECT-GUIDE.md`, `prompts-template.md`, and uninstantiated `*-TEMPLATE.md`
    copies before committing `T-000`).
    Stop after step 3 of the guide and report before starting the task loop.
    Verify before reporting: every command in AGENTS.md → Project snapshot runs
    as written, including the cold-checkout gate.
    Budget: main-loop only, unless a step is a broad mechanical sweep — then at
    most ⟨N⟩ ⟨haiku/sonnet⟩ subagents per AGENTS.md → Sub-agents and budget.
    Commit locally as the guide directs; never push without my explicit approval;
    ask before anything destructive or outward-facing.
    Stop early if blocked on a decision only I can make — record the question per
    AGENTS.md → Blockers, questions, escalation and end cleanly.
    Report: what was created; every command run with its observed result (proven
    vs. inferred, labeled); the seeded TASKS.md backlog for my review.

### Variant A2 — from a central kit clone

    Create a new project at ~/⟨ProjectName⟩.

    Follow ⟨kit path⟩/templates/NEW-PROJECT-GUIDE.md,
    using the templates in that folder as its step 1 directs.

    Product goal: ⟨one sentence — what this is and for whom, or "see idea.md"⟩.
    Stack: ⟨language / framework — or "propose one and say why before scaffolding"⟩.
    Platforms: ⟨macOS / Linux / Windows / iOS / …⟩.
    Hard constraints: ⟨licenses, dependencies to avoid, privacy rules, offline-first, …⟩.
    Autonomous loops later: ⟨yes — adopt LOOP.md as the guide directs | no⟩.

    Ask clarifying questions first for anything underspecified before locking
    docs/PLAN.md. Stop after step 3 of the guide and report before starting the task loop.
    Verify before reporting: every command in AGENTS.md → Project snapshot runs
    as written, including the cold-checkout gate.
    Budget: main-loop only, unless a step is a broad mechanical sweep — then at
    most ⟨N⟩ ⟨haiku/sonnet⟩ subagents per AGENTS.md → Sub-agents and budget.
    Commit locally as the guide directs; never push without my explicit approval;
    ask before anything destructive or outward-facing.
    Stop early if blocked on a decision only I can make — record the question per
    AGENTS.md → Blockers, questions, escalation and end cleanly.
    Report: what was created; every command run with its observed result (proven
    vs. inferred, labeled); the seeded TASKS.md backlog for my review.

---

## Scaffold B — task-execution session (the everyday one)

    Work in ~/⟨ProjectName⟩.

    Session start: run AGENTS.md → Session ritual (Start) in full, in order,
    including the git log / git status clean-tree check — stop and report if the
    tree is dirty or a stale claim needs handling.

    Task: ⟨T-### — title | pick the next eligible per AGENTS.md → The task loop⟩.
    Run AGENTS.md → The task loop, all ten steps PICK→NEXT, as written — do not
    substitute a shortened version. Deviations go in goose-deuce.md per its rules,
    in the same commit.

    Do at most ⟨1⟩ task(s) this session.
    Verify with ⟨the full gate from AGENTS.md → Project snapshot, spelled out,
    e.g. `uv run pytest --cov --cov-fail-under=80 && uv run ruff check . &&
    uv run ruff format --check . && uv run mypy src`⟩ before every commit; never
    commit red.
    Budget: ⟨main-loop only | at most N haiku/sonnet subagents for mechanical
    sweeps, their output reviewed and re-tested before it touches the tree⟩.
    Commit locally; never push without my explicit approval. Ask before anything
    destructive or outward-facing.
    Stop when: the task budget is spent; or you are blocked on a decision only I
    can make; or PICK finds nothing eligible — in every case record state per
    AGENTS.md (blocked question / board report / smallest unblocking decision),
    do not invent work, and end the session cleanly.
    Report, per task: what shipped; test evidence (command + observed result,
    proven vs. inferred, labeled); docs touched; deviations logged (date + title)
    or "none"; TASKS.md status for every task touched.

---

## Scaffold C — review / audit session

    Review ⟨the working-tree diff | branch NAME against main | subsystem/path⟩
    in ~/⟨ProjectName⟩.

    Read AGENTS.md first — its standards in full are the review bar; the lenses
    below are where to look hardest, not the whole bar.

    Mode: ⟨findings only — modify nothing | fix — apply findings via AGENTS.md →
    The task loop, one finding = one task = one commit⟩.
    Lenses: ⟨correctness, security, data loss, cross-platform, comment/doc
    honesty — comments asserting the unexercised are findings⟩.
    Verify every finding before reporting it: reproduce it (a failing test,
    command output, or a traced path with file:line). Label each CONFIRMED
    (reproduced — "proven" in AGENTS.md → Reporting standards terms) or PLAUSIBLE
    (argued, not reproduced — "inferred"); never report PLAUSIBLE as fact.
    Budget: ⟨at most N⟩ subagents as adversarial verifiers.
    Commit locally (fix mode only); never push without my explicit approval. Ask
    before anything destructive or outward-facing.
    Stop when: the lens list is exhausted, or a finding needs a decision only I
    can make — file it and end the session cleanly.
    Report: findings ranked by severity, each with file:line, the failure
    scenario, CONFIRMED/PLAUSIBLE, and the smallest fix. In fix mode, also the
    Scaffold-B per-task report for every fix applied. No praise, no padding.
    "No findings" is a valid result only after stating what was checked and how.

---

## Scaffold D — sweep session (the recurring one)

    Work in ~/⟨ProjectName⟩.

    Session start: run AGENTS.md → Session ritual (Start) in full.

    Task: the standing goose-deuce sweep item (T-⟨###⟩). Run it as board work:
    the sweep actions in goose-deuce.md → Rules → "The sweep", then the full
    audit checklist in step 5 of
    https://github.com/SnoobieJunes/goose-deuce → templates/NEW-PROJECT-GUIDE.md.
    File review findings as TASKS.md items in your own commits — no drive-by
    fixes. Close the sweep with its [process] marker entry and file the next
    sweep task.

    Commit locally; never push without my explicit approval.
    Report: the date range swept; every Plan: adjustment folded into docs/PLAN.md;
    orphaned [deferred]/[tech-debt] items restored; audit findings filed (task
    IDs); the stranger-test result.

---

## Scaffold E — Hermes session (task-execution, Hermes-native)

    Work in ~/⟨ProjectName⟩.

    Session start: resume the project's Hermes session (`hermes --resume latest` / `hermes -c` or the
    desktop session list) and run AGENTS.md → Session ritual (Start) in full,
    including the git log / git status clean-tree check — stop and report if the
    tree is dirty or a stale claim needs handling. Read HERMES-OVERLAY.md after
    the ritual (Hermes-native rules). Memory is loaded by the runtime; treat it
    as a cache — project truth is always re-read from the files.

    Task: ⟨T-### — title | pick the next eligible per AGENTS.md → The task loop⟩.
    Run AGENTS.md → The task loop, all ten steps PICK→NEXT, as written. Deviations
    go in goose-deuce.md per its rules, in the same commit.

    Do at most ⟨1⟩ task(s) this session.
    Verify with ⟨the full gate from AGENTS.md → Project snapshot⟩ before every
    commit; never commit red.
    Budget: ⟨main-loop only | at most N subagents via delegate_task for mechanical
    sweeps, their output reviewed and re-tested before it touches the tree⟩.
    Delegate to the cheapest sufficient model tier (fast/cheap tier for routine
    mechanical work, stronger tier for architecture and hard debugging, frontier
    tier for final sign-off with human approval required).
    Commit locally; never push without my explicit approval. Ask before anything
    destructive or outward-facing.
    Stop when: the task budget is spent; or you are blocked on a decision only I
    can make; or PICK finds nothing eligible — in every case record state per
    AGENTS.md, do not invent work, and end the session cleanly.
    Report, per task: what shipped; test evidence (command + observed result,
    proven vs. inferred, labeled); docs touched; deviations logged (date + title)
    or "none"; TASKS.md status for every task touched; which model tier ran it.

---

## Worked example — scaffold B, filled

    Work in ~/projects/fieldnotes.

    Session start: run AGENTS.md → Session ritual (Start) in full, in order,
    including the git log / git status clean-tree check — stop and report if the
    tree is dirty or a stale claim needs handling.

    Task: T-012 — Reject a CSV whose header row appears twice.
    Run AGENTS.md → The task loop, all ten steps PICK→NEXT, as written — do not
    substitute a shortened version. Deviations go in goose-deuce.md per its rules,
    in the same commit.

    Do at most 1 task this session.
    Verify with `uv run pytest --cov --cov-fail-under=80 && uv run ruff check .
    && uv run ruff format --check . && uv run mypy src` before every commit;
    never commit red.
    Budget: main-loop only — no subagents.
    Commit locally; never push without my explicit approval. Ask before anything
    destructive or outward-facing.
    Stop when: the task is done; or you are blocked on a decision only I can
    make; or PICK finds nothing eligible — in every case record state per
    AGENTS.md, do not invent work, and end the session cleanly.
    Report: what shipped; test evidence (command + observed result, proven vs.
    inferred, labeled); docs touched; deviations logged (date + title) or "none";
    TASKS.md status for every task touched.

---

## Anti-patterns

- **"Improve the code."** No queue item, no acceptance line — the agent invents
  its own priorities, which is exactly what TASKS.md exists to prevent.
- **Pasting standards the repo already owns.** Two sources of truth: the prompt's
  copy wins by recency, then drifts from the law. Point at AGENTS.md — the
  scaffolds' "in full, as written" lines are the pattern.
- **Unbounded scope.** "Do as much as you can" ends in half-done tasks at context
  exhaustion. Cap tasks per session; one is a fine default.
- **Burying the task.** Location, session start, task — in the first five lines.
  Everything else is modifier.