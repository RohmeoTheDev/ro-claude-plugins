---
name: sync-claude-plugin
description: Publish the Cursor slash-command pack as Claude account skills (Desktop Chat / Cowork / claude.ai) via the ro-claude-plugins marketplace
disable-model-invocation: true
---

<!-- Generated from .cursor/commands/sync-claude-plugin.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# /sync-claude-plugin

You are in the **Ro AI Base** meta launcher workspace.

Claude has three loaders. Claude Code and the Desktop **Code** tab read
`~\.claude\commands` (kept by `sync-claude-commands.ps1 -User`). Desktop
**Chat / Cowork / Projects** and claude.ai only load skills + plugins enabled on
the claude.ai account - they never read `~\.claude`. This command feeds that
second group.

## Do this

1. Run:

```powershell
& "<META_ROOT>\scripts\build-claude-plugin.ps1" -Push
# preview only:
& "<META_ROOT>\scripts\build-claude-plugin.ps1" -WhatIf
# also write dist\ro.plugin.zip for a manual Customize -> Plugins upload:
& "<META_ROOT>\scripts\build-claude-plugin.ps1" -Push -Zip
```

Resolve `<META_ROOT>` as this workspace root.

What it does: reads `template/.cursor/commands/*.md` + meta ops, writes one
`skills/<name>/SKILL.md` per command into
`D:\Ro App Builds (2026)\- Ro Claude Plugins -\plugins\ro\`, bumps the plugin
`version` **only when generated content changed**, commits, pushes to
`github.com/RohmeoTheDev/ro-claude-plugins` (private).

2. Report: version, added / modified / removed skill names, pushed or unchanged.

3. If the version bumped, tell the user: Claude Desktop -> Customize -> Plugins
   -> marketplace **ro-plugins** -> **Update**, then fully quit and reopen
   Desktop. Cowork caches on that version string; an edit without a bump ships
   nothing, and an Update without a restart often shows the old copy.

4. Do **not** edit anything under `- Ro Claude Plugins -` by hand. Source of
   truth is the Cursor command file. Fix it there, re-run this.

## Rules

- Skill names drop the `-v1.00` suffix (dots are illegal in skill names):
  `ro-workflow-session-close-v1.00.md` -> `/ro:ro-workflow-session-close`.
- Every generated skill is `disable-model-invocation: true`. `/boot`,
  `/new-project`, `/ro-workflow-git-sync` must never auto-fire in a random chat.
- `install-command.ps1` already calls this with `-Push` after a backfill;
  `-NoPlugin` skips it.
- Cursor `.cursor/commands` is never touched.
