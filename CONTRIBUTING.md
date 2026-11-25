# Contributing to goose-deuce

goose-deuce is a small set of markdown templates that make AI coding agents
disciplined. The kit itself is the master: improvements that prove reusable across
projects land here by pull request, and every adopter benefits.

The process the kit teaches is the process we use to change the kit.

## The invariants — do not break these

These properties make the system work. A PR that violates one isn't ready:

1. **Single source of truth.** `AGENTS.md` owns the law — the task loop, the board
   format, standards, testing, docs, deviations, version control, and Definition of
   Done — in one file so rules never drift across copies. Overlays (`LOOP.md`,
   `HERMES-OVERLAY.md`) add only what is specific to their harness; if a proposed line
   restates an `AGENTS.md` rule, delete it.
2. **One owner per rule.** Each rule, count, and cadence (`⟨3⟩` session-start entries,
   `⟨10⟩` / `⟨weekly⟩` sweep cadence, coverage floor, token cap) lives in one place;
   everything else points there.
3. **Placeholder discipline.** `⟨…⟩` are fill-ins an adopter replaces; `<…>` inside
   fenced format specimens and inline code spans stay for the life of the repo. Never
   turn a format specimen into a fill-in, and keep `goose-deuce.md` free of `⟨…⟩`
   placeholders.
4. **Runnable gates.** Every guide step ends in an executable gate. A step whose
   output was never run is scaffolding theatre.
5. **Token budget.** `AGENTS.md` loads into every turn. Measure with `wc -c` and
   keep it honest against your target harness's context limit without bloating
   repeated prose.
6. **Proven vs. inferred.** Name what you ran and what it output. Never claim a
   template works without actually instantiating it and running the gates.

## How to propose a change

1. **Open an issue first** for anything beyond a typo: the failure mode you hit, the
   rule that broke or caused bloat, and what fixed it.
2. **Fork and branch.** One concern per PR — same scope discipline the kit teaches.
3. **Keep the voice.** Terse, imperative, honest. Explain *why* a rule exists, not
   marketing fluff.
4. **Date the header.** Bump the template's dated version line when rules or structure
   change.
5. **Run the gates.** Instantiate a throwaway repo from your changed `templates/` and
   run Step 1's gates (placeholder grep, `WORKED-EXAMPLE` grep, layout check,
   `CLAUDE.md` check) before opening the PR. Report what you ran and observed.

## What we welcome

- A real agent failure mode or foot-gun, generalized cleanly without adding bloat.
- Thin harness overlays (Cursor, Codex, Windsurf, OpenCode, etc.) that add real
  harness mechanics without duplicating `AGENTS.md`.
- Clearer gates, sharper examples, bug fixes in cross-references.

## What we will likely decline

- Restating an `AGENTS.md` rule in another file "for safety."
- Adding scripts, wrappers, or runtime dependencies to the pure-markdown kit.
- Weakening core rigor (e.g. making timestamped comments or per-task changelogs optional).
- Tool-specific or personal setup leaking into the harness-agnostic core.

## License

By contributing, you agree your contributions are licensed under the MIT License
that covers this repository (see [LICENSE](LICENSE)).
