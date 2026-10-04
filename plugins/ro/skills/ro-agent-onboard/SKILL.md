---
name: ro-agent-onboard
description: Orient a fresh agent session in this workspace before it starts work
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-agent-onboard-v1.00.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

You're joining an existing workspace. Before doing anything else, get yourself
up to speed by reading the files below. **Actually read them — don't skim, and
don't infer from filenames.** If a file doesn't exist, skip it silently. If a
file points to other files, follow the trail.

## 1. Orientation (read first, in this order)

- `SESSION_LOG.md` — how the last session ended. **CLOSED CLEAN** = docs synced
  and git pushed, safe fresh start; **CLOSED DIRTY** = surface the reason at the
  top of your report before anything else
- `STATE.md` — current objective / done / next / open questions (rewritten, not
  appended — this is "now")
- `GOTCHAS.md` — traps (symptom → cause → fix). Highest-value; cannot be derived
  from the codebase
- `DECISIONS.md` — dated ADRs (chose X over Y because Z)
- `README.md` — canonical project overview
- `AGENTS.md`, `CLAUDE.md`, `.cursor/rules/*`, `.clinerules`, `.windsurfrules` —
  instructions written specifically for AI agents
- `BOOT_PROMPT.md`, `HANDOFF.md`, `ONBOARDING.md`, `CONTRIBUTING.md` — anything
  that screams "read me first"
- `CHANGELOG.md`, `HISTORY.md`, `NOTES.md` — recent decisions and what's in flight
- `SKILLS.md` and everything under `skills/`, `.claude/skills/`, or
  `.cursor/skills/` — capabilities and conventions the agent is expected to know

## 2. Build, run, and dependencies

- Manifest: `package.json`, `requirements.txt`, `pyproject.toml`, `Cargo.toml`,
  `go.mod`, `Gemfile`, etc. — note the language, version, and key deps
- Entrypoints: `Makefile`, `justfile`, `Taskfile.yml`, npm/pnpm scripts, `run.py`,
  `main.*`
- Environment: `.env.example` (read), `.env` (do not read), `config/`
- Containers / runtime: `Dockerfile`, `docker-compose.yml`, `devcontainer.json`
- CI/CD: `.github/workflows/*`, `.gitlab-ci.yml`, `bitbucket-pipelines.yml`

## 3. Code map

- `ls` the repo root and every top-level source directory (`src/`, `lib/`,
  `app/`, `docs/`, `work/`, `data/`, etc.)
- Open the entrypoint(s) referenced from the README or package scripts
- Note any `TODO`, `FIXME`, `HACK`, or `XXX` markers near the entrypoints

## 4. Recent activity

- `git log -20 --oneline` — recent commits
- `git status` — what's currently modified or untracked
- Any `WIP`, `DRAFT`, `SCRATCH`, or dated files (e.g. `2026-05-16-*`) in the tree

## 5. Report back

Reply with, in this order:

1. **What this project does** — one paragraph, plain English
2. **How to build / run / test** — the exact command you'd use to verify a change
3. **Top 3 files** most relevant to typical work here, with one line each on why
4. **In-flight work** — anything half-finished, recently changed, or in
   transition; lead with `STATE.md`, then the latest `Next up` from `SESSION_LOG.md`
5. **Open questions or contradictions** — anything the docs disagree on, or that
   you'd want clarified before touching code

**Do not start any actual work until I confirm your summary.** If you're tempted
to start coding because the task feels obvious, that's the signal to stop and
post the summary first.

**Unbooted project:** if `AGENTS.md` still contains `<!-- FILL`, do not treat this
as a normal onboard. Tell the user to run `/boot` in **this** folder. Grill-me is
Phase 1 of `/boot`. Do not grill from a different workspace.
