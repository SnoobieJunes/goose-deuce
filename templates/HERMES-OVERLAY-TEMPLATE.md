# HERMES-OVERLAY.md — Hermes-native rules on top of AGENTS.md

<!-- TEMPLATE — copy to <repo>/HERMES-OVERLAY.md, fill every ⟨…⟩, delete these
     comments. Master: https://github.com/SnoobieJunes/goose-deuce (templates/HERMES-OVERLAY-TEMPLATE.md)
     Template version 1.1 (2026-11-21): genericized master URL and fixed minor
     Hermes CLI/precedence wording, no rule changes.
     Template version 1.0 (2026-10-23). Changes to the master get a dated line here.

     This is a thin overlay, shaped exactly like LOOP.md: AGENTS.md owns the law —
     the task loop, TASKS.md, standards, testing, docs, deviations, version control.
     This file adds ONLY what is true because the harness is Hermes Agent, and it
     points back to AGENTS.md for everything else. If a line here looks like it
     restates an AGENTS.md rule, delete it — the overlay must add, never duplicate.

     Wire it up: add one hook line to AGENTS.md → Session ritual (see bottom).
     Do NOT name this file `.hermes.md` or `HERMES.md` — Hermes loads context
     files first-match-wins (`.hermes.md` → `AGENTS.md` → `CLAUDE.md`), so
     `.hermes.md` suppresses loading AGENTS.md altogether and splits the single
     source of truth. This file is read by pointer, like LOOP.md and goose-deuce.md.

     Placeholders: ⟨value⟩ → fill or delete; ⟨A | B⟩ → keep one; ⟨If X: …⟩ → keep
     unbracketed if X holds else delete the line. After instantiation
     `grep -n "⟨" HERMES-OVERLAY.md` returns nothing. -->

AGENTS.md rules all apply, unabridged. This file is true only because the harness
is Hermes Agent. Its additions:

1. **Memory boundary.** Hermes persists memory across sessions and injects it into
   every turn (the `memory` tool). Project state — the board, deviations, the plan,
   claims, park notes — lives ONLY in the repo files (TASKS.md, goose-deuce.md,
   docs/PLAN.md): portable, auditable, multi-agent-safe. Hermes memory holds only
   cross-project durable facts (owner identity, machine/env facts, standing
   conventions, foot-guns that recur across repos). Never write project-specific
   state to Hermes memory — it is not portable, it leaks into other projects, and
   it is not in the commit audit trail. A "foot-gun" that is repo-specific stays in
   AGENTS.md's snapshot; one that recurs across repos is proposed to the masters
   (AGENTS.md → Maintaining this file), not parked in memory.

2. **Session start.** Resume the project's own Hermes session (`hermes --resume latest` / `hermes -c`,
   or the desktop session list) rather than starting cold. Hermes memory is loaded
   by the runtime — do not re-derive it, but treat it as a cache: project truth is
   always re-read from the files (run AGENTS.md → Session ritual in full). Memory
   and the files may never disagree; if they do, the files win and the memory entry
   is corrected.

3. **Delegation = `delegate_task`.** Sub-agents are spawned with the `delegate_task`
   tool; it is the mechanism behind AGENTS.md → Sub-agents and budget. Default
   concurrency is ⟨N⟩ children; for a broad mechanical sweep spawn them in parallel
   and re-test every result before it touches the tree (unchanged from AGENTS.md).
   For long-running autonomous work (hours/days), spawn `hermes` processes via tmux
   per LOOP.md instead of a long delegate loop. A sub-agent's self-report is not
   proof — verify against the gate.

4. **The sweep = a scheduled `cronjob`.** The standing sweep (AGENTS.md →
   Deviations cadence) may run as a Hermes cronjob (`cronjob_manage`) pointed at the
   repo, in addition to the cadence line. A scheduled sweep is board work per
   goose-deuce.md → Rules; it commits like any sweep and NEVER pushes (the never-push
   policy is unchanged). If no cronjob is configured, the cadence line in AGENTS.md
   governs as written.

5. **Cross-project improvements = skills.** When a procedure proves reusable across
   projects, its Hermes-native home is a skill (`skill_manage`, installed under
   $HERMES_HOME/skills, loaded on relevance) — proposed to the owner as a diff,
   applied on approval, exactly like the master templates. Repo files stay the
   source of project law; a skill carries the repeatable procedure, never the law.

⟨If the repo uses tool servers: 6. **MCP servers** load with the session (`hermes
mcp list`); a new tool server added for this repo is a goose-deuce.md trigger, the
same as a new package.⟩

**Approval posture.** Hermes `approvals.mode`, `memory.write_approval`, and the security settings are the
runtime enforcement behind AGENTS.md → Version control and → Blockers. Destructive
or outward-facing actions (push, release, delete, purchase, anything leaving the
machine) require explicit human approval every time — the Hermes approval prompt
backs this rule, but the rule lives in AGENTS.md; do not rely on the prompt alone.

**Stop / park.** On context exhaustion or a block, park per AGENTS.md → Blockers
(park note → board-only commit → stash). Hermes conversation state does not survive
a restart as work state — the park note in TASKS.md is the source of truth, not the
session transcript. The next session resumes from the note.

**Token budget.** This overlay is read every Hermes session via the hook. Keep it
thin — it adds only Hermes-native rules; everything else points at AGENTS.md.

---

Hook line to add to AGENTS.md → Session ritual (step 6 area), unbracketed when this
file is adopted:

    ⟨If working in Hermes: after this ritual, read HERMES-OVERLAY.md — its rules
     add to, never replace, this file.⟩
