---
name: ro-1-1-onboard
description: Start of the session. Read first. Do not start work until the summary is confirmed.
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-1.1-onboard.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# 1.1 Onboard

Start of the session. Read first. Do not start work until the summary is confirmed.

Type `/ro-` in the menu. Session commands sort in run order: this one, learnings and docs, handover, close.

## Context
$ARGUMENTS

## Read these, in this order

Actually read them. Do not infer from filenames. If a file is missing, skip it. If it points at other files, follow the trail.

### Learnings and now (highest value — read before the code)

These are what previous sessions stored so you don't repeat traps:

- `SESSION_LOG.md` — how the last session ended. **CLOSED CLEAN** = docs synced and git pushed. **CLOSED DIRTY** = say why at the top of your report before anything else
- `STATE.md` — current objective / done / next / open questions. This is "now"
- `GOTCHAS.md` and `docs/GOTCHAS.md` — traps (symptom → cause → fix). Also read `work/**/GOTCHAS.md` for any tool this session will touch
- `DECISIONS.md` and `docs/DECISIONS.md` — dated choices. Read them. Do not treat a topic-scoped decisions file as a general log

### Project

- `README.md`
- `AGENTS.md`, `CLAUDE.md`, `.cursor/rules/*`, `.clinerules`, `.windsurfrules`
- `BOOT_PROMPT.md`, `HANDOFF.md`, `ONBOARDING.md`, `CONTRIBUTING.md`
- `CHANGELOG.md`, `HISTORY.md`, `NOTES.md`
- `SKILLS.md` and everything under `skills/`, `.claude/skills/`, `.cursor/skills/`

### Build, run, dependencies

- Manifests: `package.json`, `requirements.txt`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `Gemfile`
- Entrypoints: `Makefile`, `justfile`, `Taskfile.yml`, npm scripts, `run.py`, `main.*`
- `.env.example` (read). `.env` (do not read). `config/`
- `Dockerfile`, `docker-compose.yml`, `devcontainer.json`
- `.github/workflows/*`, `.gitlab-ci.yml`, `bitbucket-pipelines.yml`

### Code map and recent activity

- List the repo root and top-level source dirs (`src/`, `lib/`, `app/`, `docs/`, `work/`, `data/`)
- Open the entrypoint the README or package scripts name
- Note `TODO` / `FIXME` / `HACK` / `XXX` near those entrypoints
- `git log -20 --oneline` and `git status`
- Any `WIP`, `DRAFT`, `SCRATCH`, or dated files

## Report back

1. **What this project does** — one paragraph
2. **How to build / run / test** — the exact command you'd use to verify a change
3. **Top 3 files** — one line each
4. **In-flight work** — lead with `STATE.md`, then the latest `Next up` in `SESSION_LOG.md`
5. **Open questions or contradictions**

**Do not start work until the summary is confirmed.**

**Unbooted project:** if `AGENTS.md` still contains `<!-- FILL`, tell the user to run `/boot` in this folder. Do not grill from a different workspace.

## Rest of the session

- Mid-session, learnings or a doc sync, no commit: `/ro-2.1-learnings-and-docs`
- Stopping mid-task, with a paste prompt for the next agent: `/ro-3.1-handover`
- End of chat: `/ro-4.0-close` (learnings + log + git push, one command)
