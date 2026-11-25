# LOOP.md — protocol for `/loop` and autonomous sessions

<!-- TEMPLATE — copy to <repo>/LOOP.md, fill every ⟨…⟩, delete these comments.
     Master: https://github.com/SnoobieJunes/goose-deuce (templates/LOOP-TEMPLATE.md)
     Template version 2.1 (2026-11-21): genericized master URL, no rule changes.
     Template version 2.0 (2026-08-16): rebuilt as a thin overlay on AGENTS.md —
     the loop no longer carries its own workflow; AGENTS.md owns the task loop,
     the queue, the commit format, and the push policy. v1's five properties
     survive, now mostly by pointer: one item finished completely; one named
     queue (TASKS.md); exact verification commands with their foot-gun flags;
     never end red + adversarial re-read before commit; docs swept in the same
     commit.

     Wire it up: AGENTS.md → Session ritual carries a pre-built conditional line
     for exactly this ("⟨If the repo runs autonomous loops: … read LOOP.md
     …⟩") — keep it, unbracketed, when instantiating AGENTS.md (CLAUDE.md points to
     AGENTS.md, so the hook lives there). Without that hook this file
     is dead weight; the hook is what makes loops read it. -->

AGENTS.md rules all apply, unabridged. One iteration = one full pass of
AGENTS.md → The task loop (all ten steps, PICK→NEXT) over one TASKS.md item —
never breadth-first, never a shortened loop. Deviations land in goose-deuce.md
per its rules, in the same commit, exactly as in an interactive session.

What a loop adds on top:

1. **Autonomy guard** — PICK skips `Gated: owner` and `Gated: hardware` items
   unless the loop was pointed at one; a loop never answers its own escalations.
2. **Verification** — fast inner loop while iterating: ⟨fast test command⟩.
   Before commit, the full gate exactly as AGENTS.md → Project snapshot writes
   it, foot-gun flags included. Red = fix or revert; never end an iteration red.
3. **Push** — loops never push product commits. Not with prior approval, not
   once, not ever: pushing is an interactive-session action under AGENTS.md →
   Version control, and blanket authorization given at launch does not survive
   into iterations. The one carve-out is AGENTS.md's own: in a multi-agent repo,
   the standing-approved claim/board bookkeeping pushes still apply — or the
   loop's claims guard nothing.
4. **Budget** — subagents per AGENTS.md → Sub-agents and budget. Don't leave an
   item half-open at context exhaustion: finish it, or park it per AGENTS.md →
   Blockers, questions, escalation before the window closes.
5. **Pace** — schedule the next wakeup only after the tree is green and
   committed.
6. **Stop** — if two consecutive iterations yield no committable work
   (everything eligible needs the owner or hardware), park the loop: report the
   board state and the smallest owner decision that unblocks it (AGENTS.md →
   The task loop → PICK), and end. A stuck loop parks itself instead of
   spinning.
7. **Untouchables** — ⟨repo-specific things a well-meaning loop would "fix":
   frozen vectors, build gates, generated files, append-only ledgers⟩.
