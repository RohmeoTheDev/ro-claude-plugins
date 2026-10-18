---
name: ro-voice-convo-store
description: "Voice convo store. Files a Raise & Scale voice note as the next numbered talk, writes the decision if it locked, then pushes to GitHub."
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-voice-convo-store.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# Voice convo store

Type `/ro-voice-convo-store`.

This files one Raise & Scale voice talk and pushes it. It is not the generic session close.

Repo: `lifesapitch/6.7.0.01-LAP-RSWAI-Strategy-Board-of-Advisors`.

## Do this

1. If `ro-conversations/` is not visible, stop. Print the talk (and the lock or the finding) as markdown he can save. Say the folder is not open. Do not claim a file was saved. Voice cannot write the repo. Run this again from Cursor, or from Cowork with this folder open.

2. List `ro-conversations/NNN-*.md`. Next `NNN` is three digits, one higher than the highest. Do not reuse a number. Do not edit an older talk. As of 2026-10-18 the highest is `003` and the next file is `004`, unless a higher file is already there.

3. Write `ro-conversations/NNN-YYYY-MM-DD-topic.md`. Title, date, purpose, the question, what he believed, what he believes now, why. Tag claims: `[ro]` `[ai]` `[doby]` `[course]`.

4. If he said it is locked: write `ro-rswai-strategy/decisions/YYYY-MM-DD-topic.md`. Write the next Strategy Now (`+.10` when a locked line changes, `+.01` for wording) and move the old one to `ro-rswai-strategy/archive/`. Point "Latest conversation" at the new talk and set the next number.

5. If it is a finding and he did not lock it: write `ro-rswai-strategy/insights/YYYY-MM-DD-topic.md`. Leave the Locked section alone.

6. Set `STATE.md` so the next talk number is one higher than the file you just wrote.

7. Commit and push to `origin`. No force-push. No secrets. If the push fails, say so and stop.

8. End with this and nothing after it:

```text
Stored.
Talk: ro-conversations/NNN-YYYY-MM-DD-topic.md
Lock or finding: <path or none>
Commit: <hash> on origin/master

Claude Desktop, then:
1. Open the Raise & Scale project. Not a blank chat.
2. Project knowledge → GitHub source → Sync.
3. The next voice chat sees this talk.
```
