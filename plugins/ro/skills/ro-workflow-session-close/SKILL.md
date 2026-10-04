---
name: ro-workflow-session-close
description: "End-of-session wrap: sync docs, rewrite STATE.md, stamp SESSION_LOG.md (archive-safety)"
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-workflow-session-close-v1.00.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# Session Close

This session is ending. Wrap it up so the **prior chat can be safely archived**:
sync docs, commit + push, and stamp `SESSION_LOG.md` at the repo root so the
next session can see at a glance that everything landed.

## Scope
$ARGUMENTS

If scope is empty, derive the session summary from this conversation and
`git status` / `git diff`. If a one-line summary is given, use it as the entry
title.

## Step 1 — Sync docs to reality

Quick pass, same spirit as `/ro-workflow-agent-handover` Step 1. Only fix what's
actually wrong:

1. **AGENTS.md / CLAUDE.md** — structure, conventions, constraints still match
   the repo. The two must stay in sync.
2. **README.md** — counts, paths, quick-start still current. Current focus points
   at `STATE.md`.
3. **MANIFEST.md** (if one exists) — every file has a row, every row has a file.
4. **CHANGELOG.md** (if one exists) — append an entry for this session's work.
   Never rewrite history.
5. **Any doc touched this session** — stale paths, dead links, wrong counts.

## Step 1.5 — Session memory

These are working files, not `work/` deliverables. Edit in place. Create from
the template stub if missing. Do not invent entries.

1. **Rewrite `STATE.md`** to now (objective, done this session, next, open
   questions). Do not append.
2. **Append `GOTCHAS.md`** — any trap discovered this session (dated, symptom →
   cause → fix). Skip if none.
3. **Append `DECISIONS.md`** — any trade-off locked this session (chose X over Y
   because Z). Skip if none.

`SESSION_LOG.md` remains the close-stamp (CLEAN/DIRTY, commit, archive-safety).
`STATE.md` is what to do next. Do not merge them.

## Step 2 — Stamp SESSION_LOG.md

`SESSION_LOG.md` lives at the **repo root**. Create it if missing. It has two
parts: a **status banner** at the top (replaced every close) and a
**newest-first entry list** below the divider (append-only — never rewrite or
delete old entries).

Write the new entry and banner now, with the commit field as `pending` — it
gets filled in during Step 3 so the stamp itself is inside the commit.

Template:

```markdown
# Session Log

> **LAST SESSION: ✅ CLOSED CLEAN — safe to archive prior chat and start fresh**
> Closed: YYYY-MM-DD HH:mm | Commit: `pending` | Pushed: pending | Docs: synced

---

## YYYY-MM-DD — one-line session summary

- **Done:** what shipped, with file paths
- **Docs updated:** files touched in Step 1 (or "none needed")
- **Commit:** `pending`
- **Next up:** concrete next steps for the fresh session (or "nothing queued")
```

## Step 3 — Git sync (if applicable)

Follow the `/ro-workflow-git-sync` PUSH_SYNC rules — same guards apply
(never force-push, never discard local work, stop on conflicts/auth failures).

1. `git fetch --all --prune`; safe pull/rebase if behind.
2. Stage all relevant changes **including `SESSION_LOG.md`**, `STATE.md`,
   `GOTCHAS.md`, and `DECISIONS.md`. Exclude secrets,
   local config, caches, generated junk.
3. Commit with a conventional message.
4. `git rev-parse --short HEAD` → replace both `pending` commit fields in
   `SESSION_LOG.md`, then `git commit --amend --no-edit`.
   **Only amend before pushing — never after.**
5. Push to upstream (and to both remotes if org + personal both exist).
6. Update the banner's `Pushed:` field to the actual remote/branch. If that
   edit happens after the push, make it a tiny follow-up `docs:` commit and
   push again — do not amend a pushed commit.

**Not a git repo / no remote:** skip the git steps, set
`Commit: n/a` and `Pushed: n/a (local only)` — the close still counts as clean
if docs + log are done.

**Blocked (conflicts, auth failure, failing checks):** stop, and set the banner
to:

```markdown
> **LAST SESSION: ⚠️ CLOSED DIRTY — do NOT archive prior chat yet**
> Reason: <what's blocking> | Fix first, then re-run /ro-workflow-session-close
```

## Step 4 — Report

Final message must state, in order:

1. Banner status: **CLOSED CLEAN** or **CLOSED DIRTY** (+ reason)
2. Commit hash + message, remotes/branches pushed
3. Docs changed in Step 1
4. The `Next up` items from `STATE.md` (and the SESSION_LOG copy)
5. Explicit line: **"Safe to archive this chat"** or **"Do not archive yet"**

## Rules

- **Never rewrite or delete prior SESSION_LOG.md entries** — banner is the only
  replaceable part.
- **No secrets, tokens, or .env values** in the log.
- **Do not start new work.** This command wraps up; if you spot a problem
  worth fixing, put it under `Next up` instead.
- If the session produced nothing to commit, still stamp the log
  (`Commit: n/a — no changes`) so the next session knows the close was
  deliberate.
