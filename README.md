# The Salience Model

**A notebook that thinks with you.**

You save what you learn. An AI helper (Claude) keeps it organized, connected, and honest. And *you* stay the boss — the AI never decides what's true or important. You do.

---

## What is a "second brain"?

Your head is great at having ideas and terrible at storing them. A **second brain** is a folder of notes that remembers things *for* you — what you read, what you decided, what you're still wondering about.

This kit is a ready-made second brain. Copy it, answer a few questions, and start saving notes.

## What makes this one different?

1. **You're the boss.** The AI drafts, organizes, and asks good questions. It never changes, promotes, or deletes anything without your OK.
2. **Notes earn their importance.** Every note starts out *normal*. If a note keeps helping you, it gets promoted to an **anchor**. If it just sits there collecting dust, it gets flagged as *disposable*. Nothing is "important" just because it was loud on the day you wrote it.
3. **It's all just text files.** Plain Markdown in a folder you own. No app can trap your notes.

## What you need

- A free [GitHub](https://github.com) account and [Git](https://git-scm.com) (this saves your history)
- [Claude Code](https://claude.com/claude-code) (the AI helper that reads your notes)
- *(Optional)* [Obsidian](https://obsidian.md) — a free app that shows your notes as a pretty, clickable web

## Set it up (about 10 minutes)

1. **Copy this kit.** Click the green **"Use this template"** button at the top of this page. Name your copy anything you like, and set it to **Private** (these will be *your* notes).
2. **Put it on your computer.**
   ```bash
   git clone https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git my-second-brain
   cd my-second-brain
   ```
3. **Start Claude Code in that folder.**
   ```bash
   claude
   ```
4. **Type `/setup`.** Claude will interview you — one easy question at a time — and build your `CORE.md`: the one page that tells the AI who you are and how you want to be challenged. You approve every word.
5. **Save your first note.** Type `/capture` and paste in an article, a decision, or a question you're chewing on. Do this with about 5 real things and you're up and running.

That's it. No daily chores. No system to maintain.

## The four commands

These slash commands are the whole interface. They're already installed — they live in the [`.claude/commands`](.claude/commands) folder of this kit, and Claude Code picks them up automatically.

| Command | What it does | The recipe file |
|---|---|---|
| `/setup` | Interviews you and writes your `CORE.md` | [setup.md](.claude/commands/setup.md) |
| `/capture` | Turns something you read or thought into a note, with your approval | [capture.md](.claude/commands/capture.md) |
| `/review` | Every month or so: shows which notes earned promotion and which went cold. You decide. | [review.md](.claude/commands/review.md) |
| `/brainstorm` | Thinking-out-loud mode. The AI pushes back hard and saves nothing unless you say so. | [brainstorm.md](.claude/commands/brainstorm.md) |

Want to change how a command behaves? Each recipe file is plain English — edit it like any other note.

## The one rule that keeps it honest

`CORE.md` is the page about *you* — your values, your blind spots, how hard you want the AI to push back. The AI reads it every single session. Re-read it every few months and fix anything that's no longer true. If that one page stays honest, everything else takes care of itself.

## Want the deep dive?

The **[Full Guide](GUIDE.md)** explains the thinking behind the system: the six note types, how "earned salience" works, the optional Obsidian setup, using it with Claude on the web, and when (and when not) to add fancier tools.

## License

[MIT](LICENSE) — do whatever you like. Attribution appreciated, not required.
