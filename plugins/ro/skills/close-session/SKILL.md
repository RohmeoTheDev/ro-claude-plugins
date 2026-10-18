---
name: close-session
description: Close the chat, push to GitHub, then print the Claude Desktop Sync click so voice can see the files.
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/close-session.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# Close session

End of the chat. In Claude Desktop this is `/ro:close-session`. In Cursor it is `/close-session`.

## Do this

1. Read `ro-4.0-close` in this same command pack and run every step. Learnings, session log, commit, push. Do not write a second git procedure. Do not force-push. Do not discard local work.

2. If the push fails, or this chat cannot see the project folder, stop. Say that in one line. Do not print the Desktop steps. Voice and a normal Claude chat cannot push. Run this from Cursor, or from Cowork with the folder open.

3. If the push succeeds, or there was nothing new to commit and the log is stamped, end the reply with this block and nothing after it:

```text
Cursor is done. Commit <hash> is on origin.
(<hash> is n/a when there was nothing to commit.)

You, in Claude Desktop. There is no second command for this part.
1. Open the project. Not Cowork. Not a blank chat.
2. Project knowledge → the GitHub source → Sync.
3. Start voice inside that project.
```

Skip step 3 when the repo has no `ro-rswai-strategy/claude-project-instructions.md`. A normal close report is enough.
