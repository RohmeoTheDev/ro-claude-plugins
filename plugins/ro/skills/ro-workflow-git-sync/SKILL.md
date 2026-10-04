---
name: ro-workflow-git-sync
description: "Auto git sync: pull when clean, commit/push when dirty (no force-push)"
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-workflow-git-sync-v1.00.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

Repo sync prompt

Mode: AUTO unless I specify PULL_ONLY or PUSH_SYNC.

Always start by inspecting the repo:

- Run `git status --short --branch`.
- Check current branch, upstream, and remotes.
- Run `git fetch --all --prune`.
- Never discard, reset, clean, or overwrite local work.
- Never force-push.
- Stop only for real blockers: conflicts, auth failure, missing upstream, failing required checks, or ambiguous remotes.

AUTO decision:

- If the repo is clean, run PULL_ONLY.
- If the repo has local changes, deleted files, untracked project files, is ahead of upstream, or I say sync/finish/end/checkpoint/push, run PUSH_SYNC.
- If I explicitly say start, pull, latest, or PULL_ONLY, only pull latest and report any unsynced local work.

PULL_ONLY path:

- Fetch all remotes.
- Report whether the branch is up to date, behind, ahead, or diverged.
- If clean and behind, pull with rebase.
- If dirty and behind, preserve local work using a safe autostash/rebase only if safe; otherwise stop and explain.
- Finish with latest commit, branch status, and whether the working tree is clean.

PUSH_SYNC path:

- First complete the safe pull/latest check.
- Review actual local changes.
- Update README, CHANGELOG, and AGENTS.md/CLAUDE.md only where needed. Do not rewrite docs wholesale.
- Add a CHANGELOG entry with today's date, a one-line summary, and concrete bullets.
- Run relevant checks/tests if discoverable.
- Stage all relevant project changes, including modified, deleted, and untracked files. Exclude secrets, local config, caches, and generated junk.
- Commit with a conventional commit message chosen automatically: feat:, fix:, docs:, or refactor:.
- Push to the configured upstream.
- If both org and personal remotes exist and are valid, push the same branch to both.
- Finish with final git status, commit hash/message, pushed remotes/branches, docs changed, and checks run.

Do not create an empty commit. Do not ask for commit-message approval unless I explicitly request review mode.
