# The Salience Model

A human-governed second brain you run with **Git + Claude Code**, with an **optional Obsidian layer**.

The idea is simple: you keep authority over what things *mean* and how much they *matter*. The AI does the labor — organizing, connecting, questioning. Weight isn't assigned once and forgotten; it's **earned through use**. And it's all plain Markdown in a Git repo, so nothing locks you in.

This repo is a starter kit. Clone it, fill in one file, and go.

---

## The five ideas it runs on

1. **Human authority, AI labor.** You decide what matters, what's true, and what gets deleted. The AI organizes, connects, and challenges — it never overrides you.
2. **Six note types, not folders of topics.** Every note is one of: `source`, `entity`, `idea`, `inquiry`, `action`, or `map`. Topics emerge later from links, not from a folder tree you design upfront.
3. **Relationships over folders.** Connections live as inline `[[wikilinks]]` inside notes. The web of links *is* the structure.
4. **Evidence stays separate from interpretation.** A note keeps what a source actually says apart from what you (or the AI) think it means — so the AI's guesses never quietly harden into your facts.
5. **Salience is earned, not assigned.** Notes are born `normal`. They get promoted to `anchor` only when they prove themselves, and demoted to `disposable` when they go dead. **Git commit history is your access log** — it records what you actually touch, so you never have to invent decay numbers.

> Why "Salience Model"? In cognitive science, *activation* (how available something is) is computed by a machine from frequency and recency; *salience* (how much it matters) is a human judgment. This system runs on the part a human can actually maintain by hand — salience — and lets Git quietly stand in for the frequency signal.

---

## What you need

**Both paths require:**

- **Git** and a **GitHub account** (or any Git host).
- **Claude Code** (the CLI). This is what reads your files, drafts notes, and runs the commands.

**Path B additionally uses:**

- **Obsidian 1.12.4 or newer**, with the built-in **Command line interface** enabled. Obsidian gives you a visual editor, graph view, and — importantly — **link-safe renames and moves**.

You do **not** need embeddings, databases, or any plugins to start. Add those only when you feel their absence (see [When to add machinery](#when-to-add-machinery)).

---

## Choose your setup

### Path A — Git + Claude Code only (simplest)

Everything is plain Markdown edited directly by Claude Code. No Obsidian, no plugins.

- **Pros:** nothing to install beyond Claude Code and Git. Dead simple. Fully portable.
- **Cons:** no visual editor or graph. If you rename/move notes by hand, you have to fix `[[wikilinks]]` yourself.
- **Best for:** getting started fast, or people who live in the terminal.

### Path B — Add Obsidian (visual front end + link-safe moves)

Same repo, same files. Obsidian sits on top as your editor and viewer, and its CLI handles the operations where link integrity matters.

- **Pros:** you can browse, edit, and see the link graph. Renaming/moving a note **auto-updates every `[[wikilink]]`** pointing at it. Property changes reindex instantly.
- **Cons:** one more app; if you use Obsidian Sync across devices, mind the [sync caveat](#a-note-on-obsidian-sync).
- **Best for:** anyone who wants to actually *read* their second brain, not just query it.

**You can start on Path A and add Obsidian later — the files don't change.**

---

## Startup: your first 15 minutes

1. **Get the repo.**

   ```bash
   # Option 1: clone this starter
   git clone https://github.com/LawsonMode/second-brain-framework.git my-second-brain
   cd my-second-brain

   # Option 2: start fresh with the same layout
   mkdir my-second-brain && cd my-second-brain && git init
   ```

2. **Confirm the layout** (see [File reference](#file-reference) for what each does):

   ```text
   my-second-brain/
   ├── CLAUDE.md              ← the constitution (auto-loads in Claude Code)
   ├── CORE.md                ← YOU fill this in (copied from CORE.template.md)
   ├── notes/                 ← one idea per file
   ├── raw/                   ← untouched sources
   ├── templates/
   │   └── note.template.md
   └── .claude/
       └── commands/
           ├── capture.md
           ├── review.md
           └── brainstorm.md
   ```

3. **Fill in `CORE.md`.** Copy `CORE.template.md` to `CORE.md` and write it honestly. This is the one file that has to be *yours* — it's what the AI reads every session to know who it's working with. Keep it under a page.

   ```bash
   cp CORE.template.md CORE.md
   ```

4. **Set 5–15 anchors** inside `CORE.md` — your non-negotiable values, principles, and commitments. Start small; you can add more later.

5. **Capture 5 real things.** Open Claude Code in the folder and run `/capture` on a few actual notes — an article, a decision, an open question. This is how you learn whether the system fits before you pour everything in.

6. **Commit.**

   ```bash
   git add . && git commit -m "Initial second brain"
   ```

**Path B users, two extra one-time steps:** open the folder as a vault in Obsidian, then enable the CLI in **Settings → General → Command line interface → Register CLI**.

---

## The prompt to paste into Claude

How much you paste depends on whether Claude can read your files.

### If you're using Claude Code inside the repo (recommended)

**You barely paste anything.** `CLAUDE.md` auto-loads every session, so the operating rules are already in context. To start working, just state your objective — or use a command:

```text
/brainstorm should I restructure my course around project-based units?
```

```text
/capture   (then paste the article or point at a file)
```

```text
/review 3 months
```

That's the whole point of `CLAUDE.md`: no fragile ritual, no re-pasting rules.

### If you're using Claude on the web (no file access)

Claude can't see your files, so you paste the operating contract **and** your `CORE.md` at the start of a session. Copy this block, then paste your filled-in `CORE.md` beneath it:

```text
You're my thinking partner for a second brain I control. Below this message I'll
paste my CORE profile — read it and follow it, especially the challenge level and
blind spots.

How we work:
- I decide what matters, what's true, and what gets deleted. You organize,
  connect, and challenge. You never override me.
- Keep EVIDENCE (what a source says) separate from INTERPRETATION (what you or I
  think it means). Never present a guess as fact. Never treat your own past
  summary as a source.
- Notes have a type: source, entity, idea, inquiry, action, or map.
- Relationships are inline [[wikilinks]], not folders.
- Salience is earned: every note starts `normal`. Suggest promoting one to
  `anchor` only when it proves itself (cited in a real decision, linked
  repeatedly). Flag `disposable` when a note is clearly dead. Never change
  salience, merge, or delete without asking me first.
- No identifiable student or sensitive personal data goes into notes. If a
  capture contains it, stop and flag it.

When I paste a source and say "capture," draft ONE note: frontmatter (type +
salience: normal), a one–two sentence summary, inline [[wikilinks]] to related
notes, and — only for ideas and inquiries — an Evidence / My-read split. Show me
the draft before finalizing.

--- MY CORE PROFILE BELOW ---
[paste the contents of your CORE.md here]
```

Then, when you're done, ask: *"Give me the final Markdown for any notes we agreed to keep,"* and paste those into your `notes/` folder yourself.

---

## Daily use

Three commands cover almost everything. In Claude Code they're slash commands; on the web, just describe the mode.

- **`/capture`** — turn a source or thought into a note. Preserves the raw source, drafts a note from the template, proposes links, waits for your approval, then commits. Never self-promotes a note to `anchor`.
- **`/review`** — the by-exception maintenance pass. Uses `git log` to find what's been added and what's gone cold, then hands you a short list of anchor candidates, dead weight, and unresolved questions. You decide every change.
- **`/brainstorm`** — high-challenge thinking mode. Capture is **off** on purpose — brainstorming is mostly chaff, and you don't want it polluting the vault. At the end it names the 2–3 ideas worth keeping and offers to `/capture` those.

**There is no daily/weekly/monthly chore.** You review a note when you happen to touch it, and run `/review` occasionally (monthly-ish is plenty). Git remembers what you can't.

---

## When to add machinery

Start manual. Add complexity only when you feel a real absence — not before.

- **~a few hundred notes:** pasting/loading relevant notes stops fitting in context. *Now* add semantic search (embeddings) so retrieval scales.
- **At that same point:** you finally have months of Git history — real data on what you actually use. *Now*, if you want automatic decay/ranking, fit it to that data (FSRS-style or a generative-agents-style memory score) instead of guessing constants.
- **One plugin at a time (Path B):** the only plugin worth adding early is **Dataview**, and only when you want queries like "list every anchor" or "notes not modified in 90 days." Resist the rest.

The correct order is: prove the manual loop → let Git log the evidence → automate the math last, from data.

---

## A note on Obsidian Sync

If you use Obsidian Sync (or iCloud/Dropbox) across devices **and** let Claude Code edit files at the same time, you can get conflict copies. Two habits prevent it: commit through Git, and don't let Claude Code edit while another device is mid-sync ("one writer at a time"). On a single machine this is a non-issue.

---

## File reference

| File | What it is | Who edits it |
|---|---|---|
| `CLAUDE.md` | The operating contract. Auto-loads in Claude Code every session. | Rarely — it's the constitution. |
| `CORE.md` | Who you are, how you want to be challenged, your anchors and blind spots. Loaded every session. | **You.** Re-read quarterly. |
| `CORE.template.md` | Blank version of the above to copy from. | — |
| `notes/` | One idea per file. Linked with `[[wikilinks]]`. | You + AI (with approval). |
| `raw/` | Untouched source material. Never overwritten. | Append-only. |
| `templates/note.template.md` | The shape of a new note. | Rarely. |
| `.claude/commands/*.md` | The `/capture`, `/review`, `/brainstorm` commands. | Rarely. |

---

## The one thing that keeps this honest

The constitution loads `CORE.md` at the start of every session, so every command inherits it — and `CORE.md` has a self-expiry line at the top. That's deliberate: the system's fidelity to *you* rests entirely on that one small file staying current. Notes can drift and it's fine. If `CORE.md` fossilizes, everything downstream drifts too — quietly and convincingly. So the real maintenance obligation isn't the notes. It's re-reading `CORE.md` every quarter and asking whether it's still you.

---

## License

[MIT](LICENSE) — do whatever you like. Attribution appreciated, not required.
