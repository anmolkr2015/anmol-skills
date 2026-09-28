---
name: handoff
description: >-
  Generate a concise session handoff document (handoff.md) in the project root
  so the next session — or another developer — can pick up cleanly. Use this
  whenever the user runs /handoff, or asks to "write a handoff", "create handoff
  notes", "document what we did", "summarize this session for next time", "hand
  this off", or wants a short status doc capturing goal, current state, changed
  files, and next steps. Prefer this over an ad-hoc summary whenever the intent
  is to persist session context to a file for later pickup.
---

# Session Handoff

Write a short, factual handoff to `handoff.md` in the **project root** (the repo/
working directory the session is about) so someone with zero context can resume
cleanly. If `handoff.md` already exists, overwrite it — it reflects the latest
state, not a running log.

## Principle

The reader is the *next session* (often you, cold, or another dev). They don't
need a narrative of the conversation — they need the current truth: what we're
trying to do, where things actually stand, which files matter, what changed, what
to avoid re-trying, and what's left. Optimize for fast, unambiguous pickup.

## Gather the facts first (don't guess)

Base the document on evidence, not memory:
- `git status`, `git diff --stat`, and `git log --oneline -10` — what actually
  changed, what's committed vs uncommitted, current branch.
- The real files touched this session and their role.
- Reverts, dead-ends, and things that were tried and abandoned — these are the
  most valuable part and the easiest to lose.
- Anything deployed/published and where (URL, environment).

If a fact isn't known, say so plainly rather than inventing it.

## Structure — exactly these six sections, in order

Start with a one-line header: the project name, date, and key coordinates that
exist (live URL, repo, environment/project id, local path). Then:

1. **Goal** — What the project/effort is and what this session set out to do. 1–3 sentences.
2. **Current state** — Where things stand right now: built/deployed/committed/pushed?
   working tree clean or dirty? anything half-done or blocked? what's verified vs untested?
3. **Active files** — The files that matter for continuing, each with a one-line role.
   Only the ones the next session will actually touch or need to understand.
4. **Changes made** — What was actually done this session, terse bullets. Group if it helps.
5. **Failed attempts / dead ends** — What was tried and reverted or ruled out, and *why*,
   so the next session doesn't repeat it. Include non-obvious gotchas (env quirks,
   ordering issues, tooling that didn't work). Omit the section only if genuinely none.
6. **Next steps** — Concrete, prioritized things to do next. Actionable, not vague.

## Style

- Short and factual. Bullets over prose. No filler, no recap of the conversation.
- Prefer specifics: real file paths, commands, IDs, numbers, commit ranges.
- A tables/backticks are fine where they add scannability (e.g. file → role).
- Aim for something readable in under a minute — typically well under a page.

## After writing

Confirm the path. If the project is a git repo, offer to commit and push it
(don't commit automatically unless the user has asked you to), so the handoff is
backed up alongside the code.
