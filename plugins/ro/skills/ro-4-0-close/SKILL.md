---
name: ro-4-0-close
description: Normal end of the chat. This is learnings, the session log, and the git sync in one command. There is no separate git-sync command. After safe to close this window, the window can close. The next...
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-4.0-close.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# 4.0 Close

Normal end of the chat. This is learnings, the session log, and the git sync in one command. There is no separate git-sync command. After **safe to close this window**, the window can close. The next `/ro-1.1-onboard` reads what this wrote.

Stopping mid-task, with a paste prompt for the next agent, is `/ro-3.1-handover`. That runs this command, then writes the prompt.

## Scope
$ARGUMENTS

Empty scope = this session. A one-line summary becomes the log title.

## Step 1 — Learnings

Run the full `/ro-2.1-learnings-and-docs` pass first (gotchas, decisions, STATE, then the doc sweep). Skip a file only when it is already current.

## Step 2 — Stamp SESSION_LOG.md

Root `SESSION_LOG.md`. Create it if missing. Replace the banner. Append a new entry. Never rewrite or delete older entries.

Write `pending` now. Step 3 fills the hash before the push.

```markdown
# Session Log

> **LAST SESSION: CLOSED CLEAN — safe to close this window**
> Closed: YYYY-MM-DD HH:mm | Commit: `pending` | Pushed: pending | Docs: synced

---

## YYYY-MM-DD — one-line session summary

- **Done:** what shipped, with file paths
- **Docs updated:** files touched in Step 1 (or "none needed")
- **Commit:** `pending`
- **Next up:** concrete next steps (or "nothing queued")
```

## Step 3 — Git sync

This step is the git sync. Never force-push. Never discard local work. Stop on conflicts or auth failure.

1. `git fetch --all --prune`. Safe pull/rebase if behind.
2. Stage the session's files, including `SESSION_LOG.md`, `STATE.md`, gotchas, and decisions. Exclude secrets, caches, generated junk.
3. Conventional commit. No empty commit.
4. `git rev-parse --short HEAD` → replace both `pending` commit fields, then `git commit --amend --no-edit`. Amend only before pushing.
5. Push upstream. If org and personal push URLs both exist, push to both.
6. Set the banner `Pushed:` field to the real remote/branch. If that edit is after the push, make a tiny follow-up `docs:` commit and push it. Do not amend a pushed commit.

**No git remote:** `Commit: n/a`, `Pushed: n/a (local only)`. Still clean if learnings and the log are done.

**Blocked:** set the banner to CLOSED DIRTY with the reason and stop.

```markdown
> **LAST SESSION: CLOSED DIRTY — do not close this window yet**
> Reason: <what's blocking> | Fix first, then re-run /ro-4.0-close
```

## Step 4 — Report

1. **CLOSED CLEAN** or **CLOSED DIRTY** (+ reason)
2. Commit hash + message, remotes pushed
3. Docs and learnings written
4. `Next up`
5. **Safe to close this window** or **Do not close yet**

Nothing to commit still gets a log stamp (`Commit: n/a — no changes`). Do not start new work.
