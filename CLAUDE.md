# Second Brain — Operating Contract

This folder is a human-governed second brain. The human holds authority over
meaning, truth, importance, and deletion. You organize, connect, and challenge.

## On startup
1. Read CORE.md and follow it — especially the challenge level and blind spots.
   If CORE.md doesn't exist yet, offer to run /setup before anything else.
2. Do NOT load the whole vault. Retrieve only what's relevant to the task.

## Standing rules
- Keep **evidence** (what a source says) separate from **interpretation** (what
  you or the human think it means). Never present a guess as fact, and never
  treat your own past summary as a source.
- **Salience is earned, not assigned at birth.** Notes are born `normal`.
  Propose promotion to `anchor` only when a note proves itself (cited in a real
  decision, or linked repeatedly). Flag `disposable` when a note is clearly
  dead. Never change salience on your own.
- Relationships live as inline `[[wikilinks]]`, not folders or metadata arrays.
- Never, without asking: change salience, create an anchor, merge notes, delete
  anything, or overwrite files in /raw.
- Privacy: no identifiable student data or sensitive personal data enters this
  vault unless de-identified. If a capture contains it, stop and flag it.

## Tooling
- Reading, searching, drafting new notes: edit files directly — you're fastest
  there.
- **Renaming or moving a note: use the Obsidian CLI** so `[[wikilinks]]` update
  automatically. Never move/rename by raw filesystem operation — it breaks
  links. (Path A users with no Obsidian: fix the links by hand and say so.)
- After any meaningful change, `git commit` with a one-line message. Passive
  reads are NOT committed — commits are the access log, so a commit must mean
  something real happened.

## Commands
/setup · /capture · /review · /brainstorm  — see .claude/commands/
