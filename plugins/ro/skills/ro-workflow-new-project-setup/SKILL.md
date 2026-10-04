---
name: ro-workflow-new-project-setup
description: "Orient agent in a new workspace: read docs, report understanding, wait"
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-workflow-new-project-setup-v1.00.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# New Project Setup

Orient yourself in this workspace before doing any work.

## Context
$ARGUMENTS

## Instructions

Read every file listed below — actually read them, don't infer from filenames. If a file doesn't exist, skip it silently. If a file references other files, follow the trail.

### 1. Agent instructions (read first, in this order)

These define how you should behave in this workspace:

- `README.md`
- `AGENTS.md`, `CLAUDE.md`
- `STATE.md`, `GOTCHAS.md`, `DECISIONS.md`
- `.cursor/rules/*`
- `.clinerules`, `.windsurfrules`
- `BOOT_PROMPT.md`, `HANDOFF.md`, `ONBOARDING.md`, `CONTRIBUTING.md`

### 2. Recent context

What's been happening and what's in flight:

- `CHANGELOG.md`, `HISTORY.md`, `NOTES.md`
- `git log -20 --oneline`
- `git status`
- Any files with `WIP`, `DRAFT`, `SCRATCH`, or today's date in their name

### 3. Skills and conventions

What this workspace expects you to know how to do:

- `SKILLS.md`
- Everything under `skills/`, `.claude/skills/`, `.cursor/skills/`

### 4. Tech stack

Identify the language, framework, key dependencies, and how to run the project:

- Scan for: `package.json`, `requirements.txt`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `Gemfile`, `composer.json`, `pom.xml`
- Scan for: `Makefile`, `justfile`, `Taskfile.yml`, npm/pnpm scripts, `run.py`, `main.*`
- Read `.env.example` (never read `.env`)
- Scan for: `Dockerfile`, `docker-compose.yml`, `devcontainer.json`
- Scan for: `.github/workflows/*`, `.gitlab-ci.yml`, `bitbucket-pipelines.yml`

### 5. Code map

Understand the shape of the codebase:

- List the repo root and every top-level source directory (`src/`, `lib/`, `app/`, `docs/`, `work/`, `data/`, etc.)
- Open the entrypoint(s) referenced from README or package scripts
- Note any `TODO`, `FIXME`, `HACK`, or `XXX` markers near entrypoints

### 6. Report back

Reply with exactly these five sections, in this order:

1. **What this project does** — one paragraph, plain language
2. **How to build / run / test** — the exact commands to verify a change
3. **Top 3 files** — most relevant to typical work here, one line each explaining why
4. **In-flight work** — anything half-finished, recently changed, or in transition
5. **Open questions** — anything the docs disagree on, anything unclear, anything you'd want answered before touching code

**Do not start any work until I confirm your summary.** If the task feels obvious and you're tempted to just start — that's the signal to stop and post the summary first.
