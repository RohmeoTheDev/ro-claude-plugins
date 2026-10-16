---
name: ro-2-1-learnings-and-docs
description: Two jobs, no commit. Store what this session learned, then sync the docs that session made stale. Run any time, including mid-session. It does not commit, push, or close the chat. /ro-4.0-close runs...
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-2.1-learnings-and-docs.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# 2.1 Learnings and docs

Two jobs, no commit. Store what this session learned, then sync the docs that session made stale. Run any time, including mid-session. It does **not** commit, push, or close the chat. `/ro-4.0-close` runs this, then stamps the log and pushes.

## Scope
$ARGUMENTS

Empty scope = this whole session. A path or topic limits both passes to that area.

## 1. Learnings

Only real lessons. If nothing new came up, say so. Do not invent filler.

1. **Gotchas** — symptom → cause → fix. Write `docs/GOTCHAS.md` if that file exists, otherwise root `GOTCHAS.md`. Mirror the same lesson into the matching `work/**/GOTCHAS.md`. Keep both in sync. Next `G-NNN` id when the file uses that scheme.
2. **Decisions** — chose X over Y because Z. Append to `docs/DECISIONS.md` or root `DECISIONS.md` only when that file is a general decision log. If it is scoped to another topic, do not dump into it. Put the decision in `STATE.md` instead and say why.
3. **STATE.md** — rewrite, don't append. Objective, done, next, open questions. This file is "now".

## 2. Docs

Truth is the code. Fix what this session made stale, wrong, missing, or broken. Do not restyle. Do not crawl every markdown file under `work/`. Do not guess: if you cannot confirm a fact, leave `<!-- TODO(learnings): ... -->`.

Check these, and edit only what drifted:

1. **AGENTS.md / CLAUDE.md** — tool facts, conventions, paths, command names. Those two stay identical. After editing one, copy it to the other.
2. **README.md** — counts, paths, quick-start, structure table.
3. **docs/** — files this session invalidated (`CONTEXT.md`, plans, anything an agent reads). Dead links, wrong versions, wrong command names.
4. **Tool README** under `work/**` for any tool this session changed.
5. **MANIFEST.md** beside a command package, if commands changed. Every file has a row. Every row has a file.
6. **CHANGELOG.md** — append when behaviour or a tool changed. Never rewrite, reorder, or delete history.
7. **`.env.example`** — names only, if code started reading a new var. Never read `.env`. Never paste values.

Skip vendored trees, `node_modules/`, archives, and secrets.

## Do not

- Do not stamp `SESSION_LOG.md` as closed, and do not commit or push. Both happen inside `/ro-4.0-close`.
- Do not start new work.

## Report

- Learnings captured, or "none this session"
- Docs changed, one line each, or "docs already current"
- Anything you refused to put in a scoped decisions file
- Every `<!-- TODO(learnings): ... -->` left behind
