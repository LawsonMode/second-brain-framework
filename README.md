# Second Brain Framework

A starter template for an **LLM-maintained personal wiki** — a "second brain" where you curate sources and ask questions, and an AI agent (Claude Code, or any coding-agent that reads `CLAUDE.md`-style instructions) does the tedious bookkeeping: summarizing, cross-linking, contradiction-flagging, and index maintenance.

Built on Andrej Karpathy's [LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f). The core idea: instead of re-reading raw documents on every question (RAG-style), the LLM incrementally builds and maintains a **persistent, compounding wiki**. Synthesis happens **once, at ingest**, then stays current.

## What you get

```
your-vault/
├── CLAUDE.md              ← the schema: rules your AI agent follows
├── Nexus.md               ← home page / catalog (every page reachable from here)
├── log.md                 ← changelog of every AI edit
├── Verification Queue.md  ← open questions awaiting real-world answers
├── sources/               ← immutable raw material (yours; the AI never edits it)
│   └── inbox/             ← drop zone for new, not-yet-ingested files
├── wiki/
│   ├── topics/            ← hub pages that map an area
│   ├── concepts/          ← one idea per page
│   ├── entities/          ← orgs, tools, projects, places
│   ├── people/            ← one page per human — the CRM layer
│   └── summaries/         ← one page per raw source
└── _templates/            ← page templates for each type
```

The vault is plain Markdown with `[[wikilinks]]`, so it works beautifully in [Obsidian](https://obsidian.md) — but Obsidian is optional. Any text editor works.

## Quickstart

1. **Click "Use this template"** on GitHub (or clone this repo) to create your own vault. Make your copy **private** — it will hold your personal notes.
2. **Open the folder with your AI agent.** With [Claude Code](https://claude.com/claude-code): `cd your-vault && claude`. The agent reads `CLAUDE.md` automatically and learns the rules.
3. **Drop something into `sources/inbox/`** — an article you saved as Markdown, meeting notes, a transcript, anything.
4. Tell the agent: **"Process the inbox."** It writes a summary page, creates or updates the concept/entity pages the source touches, links everything into `Nexus.md`, and logs the change.
5. **Ask questions.** The agent answers from the wiki first, with `[[wikilinks]]` as citations, and tells you honestly when the wiki can't answer.
6. Occasionally say **"Run a lint."** The agent finds orphan pages, broken links, contradictions, stale stubs, and inbox backlog.

## The three layers

| Layer | Location | Who touches it |
|---|---|---|
| **Raw sources** | `sources/` | You add; the LLM **reads only — never edits, never deletes** |
| **The wiki** | `wiki/` | LLM creates and maintains; you read and direct |
| **The schema** | `CLAUDE.md` | You approve changes; the LLM proposes them |

This separation is the safety model: your original material is immutable, every AI change is logged, and the rules themselves only change with your sign-off.

## Capturing from other AI tools

`_templates/LLM Capture Instructions.md` contains a paste-ready prompt block for ChatGPT, Gemini, or any other assistant. It makes them output clean, frontmattered Markdown you can drop straight into `sources/inbox/` — so conversations elsewhere still feed your second brain.

## Privacy notes

- Keep your vault repo **private**. This template is public; your filled-in copy should not be.
- The schema forbids the agent from creating pages about people whose data you shouldn't store (see the Privacy section of `CLAUDE.md` and adapt it to your situation — e.g., minors, patients, clients under NDA).
- `.gitignore` already excludes per-machine Obsidian state.

## Customizing

`CLAUDE.md` is versioned (semver). Change the folder map, add page types, tighten the rules — it's your brain. The only advice: keep the three-layer separation and the log. They're what keep an LLM-maintained wiki trustworthy.

## License

MIT — see [LICENSE](LICENSE).
